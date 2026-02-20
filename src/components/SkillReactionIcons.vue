<template>
  <div
    class="relative w-full max-w-4xl aspect-square rounded-3xl border border-slate-800 bg-slate-900/30 shadow-xl overflow-hidden select-none"
  >
    <canvas
      ref="canvasRef"
      class="w-full h-full block"
      @pointerdown="onPointerDown"
      @pointermove="onPointerMove"
      @pointerup="onPointerUp"
      @pointercancel="onPointerUp"
      @pointerleave="onPointerUp"
    ></canvas>

    <div
      class="pointer-events-none absolute left-4 top-4 text-xs text-slate-300/90 bg-slate-950/40 border border-slate-800 rounded-full px-3 py-1"
    >
      Drag nodes • billiards collisions • click to energize
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount, watch } from "vue";

/**
 * skills: [{ key, src }]
 * Use local assets (recommended) to avoid canvas CORS issues.
 */
const props = defineProps({
  skills: {
    type: Array,
    default: () => [
      { key: "laravel", src: "/icons/laravel.svg" },
      { key: "vue", src: "/icons/vue.svg" },
      { key: "mysql", src: "/icons/mysql.svg" },
      { key: "docker", src: "/icons/docker.svg" },
      { key: "git", src: "/icons/git.svg" },
      { key: "dotnet", src: "/icons/dotnet.svg" },
      { key: "redis", src: "/icons/redis.svg" },
      { key: "linux", src: "/icons/linux.svg" },
      { key: "tailwind", src: "/icons/tailwind.svg" },
    ],
  },

  // Motion
  minSpeed: { type: Number, default: 30 }, // px/sec
  maxSpeed: { type: Number, default: 80 }, // px/sec
  friction: { type: Number, default: 0.999 }, // velocity damping per frame-ish

  // Collisions
  restitution: { type: Number, default: 0.98 }, // 1 = perfectly elastic
  iterations: { type: Number, default: 2 }, // collision solver passes (2 is enough)

  // Links / reaction
  bondDistance: { type: Number, default: 190 },
  chainGain: { type: Number, default: 0.02 },
  energyDecay: { type: Number, default: 0.985 },

  // Node sizing
  nodeRadius: { type: Number, default: 30 },
  radiusJitter: { type: Number, default: 8 },
  iconPadding: { type: Number, default: 10 },

  // Grayscale behavior
  grayscaleWhenIdle: { type: Boolean, default: true },
  colorThreshold: { type: Number, default: 0.08 },

  // If true: clicked stays colored permanently
  stickyReveal: { type: Boolean, default: false },

  // Click energy
  clickEnergy: { type: Number, default: 1 },
});

const canvasRef = ref(null);

let ctx = null;
let rafId = null;
let ro = null;

let nodes = [];
let imageMap = new Map();

let lastT = 0;
let dpr = 1;

// Drag state
const drag = {
  pointerId: null,
  node: null,
  // offset inside node for smooth dragging
  offsetX: 0,
  offsetY: 0,
  // for “throw” velocity
  lastX: 0,
  lastY: 0,
  lastTime: 0,
};

function rand(min, max) {
  return min + Math.random() * (max - min);
}

function getCssSize() {
  const canvas = canvasRef.value;
  if (!canvas) return { w: 0, h: 0 };
  const rect = canvas.getBoundingClientRect();
  return { w: rect.width, h: rect.height };
}

function resizeCanvas() {
  const canvas = canvasRef.value;
  if (!canvas) return;

  const { w, h } = getCssSize();
  dpr = Math.max(1, window.devicePixelRatio || 1);

  canvas.width = Math.floor(w * dpr);
  canvas.height = Math.floor(h * dpr);

  ctx = canvas.getContext("2d");
  ctx.setTransform(dpr, 0, 0, dpr, 0, 0);

  if (nodes.length) clampNodesIntoBounds();
}

function clampNodesIntoBounds() {
  const { w, h } = getCssSize();
  for (const n of nodes) {
    n.x = Math.min(Math.max(n.x, n.r), w - n.r);
    n.y = Math.min(Math.max(n.y, n.r), h - n.r);
  }
}

async function loadImages() {
  imageMap.clear();

  const loaders = props.skills.map((s) => {
    return new Promise((resolve) => {
      const img = new Image();
      // If using external domain icons:
      // img.crossOrigin = "anonymous";
      img.onload = () => resolve({ key: s.key, img, ok: true });
      img.onerror = () => resolve({ key: s.key, img: null, ok: false });
      img.src = s.src;
    });
  });

  const results = await Promise.all(loaders);
  for (const r of results) {
    if (r.ok && r.img) imageMap.set(r.key, r.img);
  }
}

function initNodes() {
  const { w, h } = getCssSize();

  nodes = props.skills.map((s, i) => {
    const r = Math.max(18, props.nodeRadius + rand(-props.radiusJitter, props.radiusJitter));

    const x = rand(r, Math.max(r + 1, w - r));
    const y = rand(r, Math.max(r + 1, h - r));

    const ang = rand(0, Math.PI * 2);
    const spd = rand(props.minSpeed, props.maxSpeed);
    const vx = Math.cos(ang) * spd;
    const vy = Math.sin(ang) * spd;

    return {
      id: i,
      key: s.key,
      src: s.src,
      x,
      y,
      vx,
      vy,
      r,
      mass: r * r, // proportional to area (good for billiards feel)
      energy: 0,
      revealed: false,
      dragging: false,
    };
  });

  // Optional: simple de-overlap pass at init
  separateOverlaps(4);
}

function pulse(node, strength = 1) {
  node.energy = Math.min(1, Math.max(node.energy, strength));
  if (props.stickyReveal) node.revealed = true;
}

function getPointerPos(e) {
  const rect = canvasRef.value.getBoundingClientRect();
  return { x: e.clientX - rect.left, y: e.clientY - rect.top };
}

function hitTest(x, y) {
  let hit = null;
  let best = Infinity;
  for (const n of nodes) {
    const d = Math.hypot(x - n.x, y - n.y);
    if (d <= n.r && d < best) {
      best = d;
      hit = n;
    }
  }
  return hit;
}

function onPointerDown(e) {
  // capture to keep receiving move even if cursor leaves canvas
  canvasRef.value.setPointerCapture?.(e.pointerId);

  const { x, y } = getPointerPos(e);
  const n = hitTest(x, y);

  if (!n) return;

  drag.pointerId = e.pointerId;
  drag.node = n;
  n.dragging = true;

  // stop it while dragging (prevents jitter)
  n.vx = 0;
  n.vy = 0;

  drag.offsetX = x - n.x;
  drag.offsetY = y - n.y;

  drag.lastX = x;
  drag.lastY = y;
  drag.lastTime = performance.now();
}

function onPointerMove(e) {
  if (drag.pointerId !== e.pointerId || !drag.node) return;

  const n = drag.node;
  const { x, y } = getPointerPos(e);

  // target position with the original grab offset
  n.x = x - drag.offsetX;
  n.y = y - drag.offsetY;

  // keep inside bounds
  const { w, h } = getCssSize();
  n.x = Math.min(Math.max(n.x, n.r), w - n.r);
  n.y = Math.min(Math.max(n.y, n.r), h - n.r);

  // estimate throw velocity from pointer movement
  const now = performance.now();
  const dt = Math.max(1, now - drag.lastTime); // ms
  const dx = x - drag.lastX;
  const dy = y - drag.lastY;
  const vx = (dx / dt) * 1000; // px/sec
  const vy = (dy / dt) * 1000; // px/sec

  // store on node (applied on release)
  n._throwVx = vx;
  n._throwVy = vy;

  drag.lastX = x;
  drag.lastY = y;
  drag.lastTime = now;

  // while dragging, push others out billiards-style
  // (soft resolve overlaps against dragged node)
  resolveDraggedCollisions(n);
}

function onPointerUp(e) {
  if (drag.pointerId !== e.pointerId) return;

  const n = drag.node;
  if (n) {
    n.dragging = false;

    // apply throw velocity (clamp)
    const maxThrow = props.maxSpeed * 2.2;
    const tvx = clamp(n._throwVx ?? 0, -maxThrow, maxThrow);
    const tvy = clamp(n._throwVy ?? 0, -maxThrow, maxThrow);

    n.vx = tvx;
    n.vy = tvy;

    delete n._throwVx;
    delete n._throwVy;

    // If it was more like a click than a drag, energize it
    // (tiny movement => treat as click)
    const moved = Math.hypot(drag.lastX - (n.x + drag.offsetX), drag.lastY - (n.y + drag.offsetY));
    if (moved < 3) pulse(n, props.clickEnergy);
  }

  drag.pointerId = null;
  drag.node = null;
  drag.offsetX = 0;
  drag.offsetY = 0;
}

function clamp(v, min, max) {
  return Math.min(Math.max(v, min), max);
}

function coverRect(srcW, srcH, dstW, dstH) {
  const srcRatio = srcW / srcH;
  const dstRatio = dstW / dstH;

  let sw = srcW, sh = srcH, sx = 0, sy = 0;

  if (srcRatio > dstRatio) {
    sh = srcH;
    sw = Math.round(sh * dstRatio);
    sx = Math.round((srcW - sw) / 2);
  } else {
    sw = srcW;
    sh = Math.round(sw / dstRatio);
    sy = Math.round((srcH - sh) / 2);
  }
  return { sx, sy, sw, sh };
}

function drawBackground(w, h) {
  const g = ctx.createRadialGradient(w / 2, h / 2, Math.min(w, h) * 0.12, w / 2, h / 2, Math.min(w, h) * 0.7);
  g.addColorStop(0, "rgba(2,6,23,0.0)");
  g.addColorStop(1, "rgba(2,6,23,0.55)");
  ctx.fillStyle = g;
  ctx.fillRect(0, 0, w, h);
}

function updateMotion(dtSec) {
  const { w, h } = getCssSize();

  for (const n of nodes) {
    if (n.dragging) continue; // dragged node is controlled by pointer

    n.x += n.vx * dtSec;
    n.y += n.vy * dtSec;

    // bounce edges
    if (n.x <= n.r) {
      n.x = n.r;
      n.vx = Math.abs(n.vx) * props.restitution;
    } else if (n.x >= w - n.r) {
      n.x = w - n.r;
      n.vx = -Math.abs(n.vx) * props.restitution;
    }

    if (n.y <= n.r) {
      n.y = n.r;
      n.vy = Math.abs(n.vy) * props.restitution;
    } else if (n.y >= h - n.r) {
      n.y = h - n.r;
      n.vy = -Math.abs(n.vy) * props.restitution;
    }

    // mild friction (scaled to dt)
    const f = Math.pow(props.friction, dtSec * 60);
    n.vx *= f;
    n.vy *= f;

    // energy decay (scaled)
    const decay = Math.pow(props.energyDecay, dtSec * 60);
    n.energy *= decay;
    if (n.energy < 0.001) n.energy = 0;
  }

  // also decay energy for dragged node
  for (const n of nodes) {
    if (!n.dragging) continue;
    const decay = Math.pow(props.energyDecay, dtSec * 60);
    n.energy *= decay;
    if (n.energy < 0.001) n.energy = 0;
  }
}

/**
 * Elastic collision between circles.
 * - Resolves overlap
 * - Exchanges velocity along normal
 * - Uses masses
 */
function solveCollisions() {
  // multiple passes makes it stable when many are packed
  for (let pass = 0; pass < props.iterations; pass++) {
    for (let i = 0; i < nodes.length; i++) {
      for (let j = i + 1; j < nodes.length; j++) {
        const a = nodes[i];
        const b = nodes[j];

        // if both are being dragged, skip (rare)
        // if one is dragged, still collide (billiards feel)
        const dx = b.x - a.x;
        const dy = b.y - a.y;
        const dist = Math.hypot(dx, dy);
        const minDist = a.r + b.r;

        if (dist === 0 || dist >= minDist) continue;

        // normalize
        const nx = dx / dist;
        const ny = dy / dist;

        // --- 1) Positional correction (push apart)
        const overlap = minDist - dist;
        // distribute correction by mass (heavier moves less)
        const invMa = 1 / a.mass;
        const invMb = 1 / b.mass;
        const invSum = invMa + invMb;

        const moveA = overlap * (invMa / invSum);
        const moveB = overlap * (invMb / invSum);

        if (!a.dragging) {
          a.x -= nx * moveA;
          a.y -= ny * moveA;
        }
        if (!b.dragging) {
          b.x += nx * moveB;
          b.y += ny * moveB;
        }

        // --- 2) Velocity impulse (elastic)
        // relative velocity
        const rvx = b.vx - a.vx;
        const rvy = b.vy - a.vy;
        const velAlongNormal = rvx * nx + rvy * ny;

        // If they are separating, don't apply impulse
        if (velAlongNormal > 0) continue;

        const e = props.restitution;

        // impulse scalar
        const jImpulse = -(1 + e) * velAlongNormal / (invMa + invMb);

        const ix = jImpulse * nx;
        const iy = jImpulse * ny;

        if (!a.dragging) {
          a.vx -= ix * invMa;
          a.vy -= iy * invMa;
        }
        if (!b.dragging) {
          b.vx += ix * invMb;
          b.vy += iy * invMb;
        }

        // Optional: spark energy on collision
        const impact = Math.min(1, Math.abs(velAlongNormal) / 450);
        if (impact > 0.1) {
          pulse(a, Math.max(a.energy, 0.35 + impact * 0.65));
          pulse(b, Math.max(b.energy, 0.35 + impact * 0.65));
        }
      }
    }

    clampNodesIntoBounds();
  }
}

/**
 * If you drag one node into another, this helps “push” neighbors away immediately
 * so it feels like billiards even while dragging (before release).
 */
function resolveDraggedCollisions(dragged) {
  for (const other of nodes) {
    if (other === dragged) continue;

    const dx = other.x - dragged.x;
    const dy = other.y - dragged.y;
    const dist = Math.hypot(dx, dy);
    const minDist = other.r + dragged.r;

    if (dist === 0 || dist >= minDist) continue;

    const nx = dx / dist;
    const ny = dy / dist;
    const overlap = minDist - dist;

    // push the OTHER away (dragged is controlled by pointer)
    other.x += nx * overlap;
    other.y += ny * overlap;

    // give other a kick away (billiards feel)
    const kick = Math.min(280, overlap * 18);
    other.vx += nx * kick;
    other.vy += ny * kick;

    // energize a bit
    pulse(other, Math.max(other.energy, 0.25));
    pulse(dragged, Math.max(dragged.energy, 0.25));
  }

  clampNodesIntoBounds();
}

/**
 * If you want to avoid ugly overlaps at init.
 */
function separateOverlaps(passes = 3) {
  for (let p = 0; p < passes; p++) {
    for (let i = 0; i < nodes.length; i++) {
      for (let j = i + 1; j < nodes.length; j++) {
        const a = nodes[i], b = nodes[j];
        const dx = b.x - a.x;
        const dy = b.y - a.y;
        const dist = Math.hypot(dx, dy);
        const minDist = a.r + b.r;
        if (dist === 0 || dist >= minDist) continue;

        const nx = dx / dist;
        const ny = dy / dist;
        const overlap = minDist - dist;

        a.x -= nx * overlap * 0.5;
        a.y -= ny * overlap * 0.5;
        b.x += nx * overlap * 0.5;
        b.y += ny * overlap * 0.5;
      }
    }
    clampNodesIntoBounds();
  }
}

function drawLinksAndPropagate() {
  const bd = props.bondDistance;

  for (let i = 0; i < nodes.length; i++) {
    for (let j = i + 1; j < nodes.length; j++) {
      const a = nodes[i];
      const b = nodes[j];
      const dx = b.x - a.x;
      const dy = b.y - a.y;
      const dist = Math.hypot(dx, dy);

      if (dist >= bd) continue;

      const proximity = 1 - dist / bd;
      const energy = Math.max(a.energy, b.energy);

      ctx.strokeStyle = `rgba(148,163,184,${0.10 + proximity * 0.42 + energy * 0.55})`;
      ctx.lineWidth = 1.2 + proximity * 0.8 + energy * 2;

      ctx.beginPath();
      ctx.moveTo(a.x, a.y);
      ctx.lineTo(b.x, b.y);
      ctx.stroke();

      // chain reaction transfer
      const transfer = props.chainGain * proximity;

      if (a.energy > b.energy + 0.12) b.energy = Math.min(1, b.energy + transfer * (a.energy - b.energy));
      else if (b.energy > a.energy + 0.12) a.energy = Math.min(1, a.energy + transfer * (b.energy - a.energy));

      // travel dot
      if (proximity > 0.25) {
        const t = performance.now() * 0.00007;
        const p = (Math.sin(t + (a.id * 7 + b.id * 11)) + 1) / 2;
        const ex = a.x + dx * p;
        const ey = a.y + dy * p;

        ctx.fillStyle = `rgba(226,232,240,${0.06 + proximity * 0.18 + energy * 0.35})`;
        ctx.beginPath();
        ctx.arc(ex, ey, 2 + energy * 2.5, 0, Math.PI * 2);
        ctx.fill();
      }
    }
  }
}

function drawNode(n) {
  const e = n.energy;
  const img = imageMap.get(n.key);

  // circle base
  ctx.beginPath();
  ctx.arc(n.x, n.y, n.r, 0, Math.PI * 2);
  ctx.fillStyle = "rgba(2,6,23,0.85)";
  ctx.fill();

  // ring
  ctx.lineWidth = 2 + e * 3;
  ctx.strokeStyle = `rgba(226,232,240,${0.35 + e * 0.65})`;
  ctx.stroke();

  // glow
  if (e > 0.05) {
    ctx.beginPath();
    ctx.arc(n.x, n.y, n.r + 8 + e * 10, 0, Math.PI * 2);
    ctx.strokeStyle = `rgba(226,232,240,${0.08 + e * 0.2})`;
    ctx.lineWidth = 10;
    ctx.stroke();
  }

  if (!img) return;

  const pad = props.iconPadding;
  const size = n.r * 2 - pad * 2;

  const showColor = props.stickyReveal
    ? n.revealed || e >= props.colorThreshold
    : e >= props.colorThreshold;

  ctx.save();

  // clip
  ctx.beginPath();
  ctx.arc(n.x, n.y, n.r - 2, 0, Math.PI * 2);
  ctx.clip();

  ctx.filter = props.grayscaleWhenIdle && !showColor ? "grayscale(1)" : "none";

  const { sx, sy, sw, sh } = coverRect(img.width, img.height, size, size);
  ctx.drawImage(img, sx, sy, sw, sh, n.x - size / 2, n.y - size / 2, size, size);

  ctx.restore();
}

function frame(t) {
  if (!ctx) return;

  if (!lastT) lastT = t;
  const dtMs = Math.min(34, t - lastT); // clamp for stability
  lastT = t;
  const dtSec = dtMs / 1000;

  const { w, h } = getCssSize();
  ctx.clearRect(0, 0, w, h);
  drawBackground(w, h);

  updateMotion(dtSec);
  solveCollisions();
  drawLinksAndPropagate();

  for (const n of nodes) drawNode(n);

  rafId = requestAnimationFrame(frame);
}

onMounted(async () => {
  resizeCanvas();
  initNodes();
  await loadImages();

  ro = new ResizeObserver(() => resizeCanvas());
  ro.observe(canvasRef.value);

  rafId = requestAnimationFrame(frame);
});

onBeforeUnmount(() => {
  if (rafId) cancelAnimationFrame(rafId);
  if (ro && canvasRef.value) ro.unobserve(canvasRef.value);
  ro = null;
});

watch(
  () => props.skills,
  async () => {
    initNodes();
    await loadImages();
  },
  { deep: true }
);
</script>
