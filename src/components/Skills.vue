<template>
  <section class="py-24 relative overflow-hidden" id="skills">
    <div
      class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[800px] h-[400px] bg-primary/5 blur-[120px] rounded-full"
    ></div>
    <div class="max-w-7xl mx-auto px-6 relative z-10">
      <div class="flex flex-col md:flex-row md:items-end justify-between mb-12 gap-6">
        <div>
          <h2 class="text-4xl font-bold mb-2">Technical Mastery</h2>
          <p class="text-slate-400">My specialized toolset for building digital products.</p>
        </div>
        <!-- <div class="flex gap-2">
          <span class="px-3 py-1 rounded-full bg-slate-800 text-xs font-semibold">Frontend</span>
          <span class="px-3 py-1 rounded-full bg-slate-800 text-xs font-semibold">Backend</span>
          <span class="px-3 py-1 rounded-full bg-slate-800 text-xs font-semibold">DevOps</span>
        </div> -->
      </div>
      <!-- <div class="grid grid-cols-2 md:grid-cols-4 lg:grid-cols-6 gap-6">
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">javascript</span>
          </div>
          <span class="font-bold text-sm">JavaScript</span>
        </div>
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">deployed_code</span>
          </div>
          <span class="font-bold text-sm">Vue.js</span>
        </div>
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">database</span>
          </div>
          <span class="font-bold text-sm">Laravel</span>
        </div>
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">smartphone</span>
          </div>
          <span class="font-bold text-sm">Flutter</span>
        </div>
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">cloud</span>
          </div>
          <span class="font-bold text-sm">AWS</span>
        </div>
        <div
          class="skill-card glass p-6 rounded-2xl flex flex-col items-center gap-4 transition-all duration-300"
        >
          <div
            class="w-14 h-14 rounded-xl bg-primary/10 flex items-center justify-center text-primary"
          >
            <span class="material-symbols-outlined text-4xl">terminal</span>
          </div>
          <span class="font-bold text-sm">Docker</span>
        </div>
      </div> -->
      <SkillReactionIcons />
    </div>
  </section>
</template>

<script setup>
import SkillReactionIcons from '@/components/SkillReactionIcons.vue';
</script>
