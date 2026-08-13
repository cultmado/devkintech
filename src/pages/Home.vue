<template>
  <!-- Navigation Bar -->
  <Navbar />

  <section class="relative min-h-screen flex items-center pt-20 grid-pattern" id="home">
    <div
      class="absolute inset-0 bg-gradient-to-b from-transparent via-background-dark/50 to-background-dark pointer-events-none"
    ></div>
    <div
      class="max-w-7xl mx-auto px-6 grid grid-cols-1 lg:grid-cols-2 gap-12 items-center relative z-10"
    >
      <div class="space-y-8">
        <div
          class="inline-flex items-center gap-2 px-3 py-1 rounded-full bg-primary/10 border border-primary/20 text-primary text-xs font-bold tracking-widest uppercase"
        >
          <span class="relative flex h-2 w-2">
            <span
              class="animate-ping absolute inline-flex h-full w-full rounded-full bg-primary opacity-75"
            ></span>
            <span class="relative inline-flex rounded-full h-2 w-2 bg-primary"></span>
          </span>
          Available for Work
        </div>
        <h1 class="text-5xl md:text-7xl lg:text-8xl font-black tracking-tighter leading-none">
          Hi, I’m
          <span class="text-transparent bg-clip-text bg-gradient-to-r from-primary to-blue-400"
            >Kinn Beredico</span
          >
          <!-- , <span class="block mt-2 text-4xl md:text-6xl text-slate-200">Software Engineer</span> -->
        </h1>
        <p class="text-xl md:text-2xl text-slate-400 max-w-xl leading-relaxed">
          <span class="text-slate-100 font-bold">Full-Stack Developer</span> building scalable systems by day and lifting heavy code (and weights) by night — engineered for performance, reliability, and gains.
          <!-- Full-stack and mobile development expert building
          <span class="text-slate-100">premium digital experiences</span> with modern technology
          stacks. -->
        </p>
        <!-- <p class="text-xl md:text-2xl text-slate-400 max-w-xl leading-relaxed">
          Full-stack and mobile development expert building
          <span class="text-slate-100">premium digital experiences</span> with modern technology
          stacks.
        </p> -->
        <div class="flex flex-wrap gap-4">
          <button
            class="bg-primary hover:shadow-[0_0_20px_rgba(13,89,242,0.4)] text-white px-8 py-4 rounded-xl font-bold flex items-center gap-2 transition-all"
          >
            Download CV <span class="material-symbols-outlined">download</span>
          </button>
          <!-- <button
            class="bg-charcoal hover:bg-slate-700 border border-slate-700 text-white px-8 py-4 rounded-xl font-bold transition-all"
          >
            Download CV
          </button> -->
        </div>
      </div>
      <div class="relative hidden lg:block">
        <div
          class="relative glass rounded-3xl p-6 -rotate-2 hover:rotate-0 transition-transform duration-500 shadow-2xl"
        >
          <div class="flex items-center gap-2 mb-5">
            <span class="w-3 h-3 rounded-full bg-red-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-yellow-500/80"></span>
            <span class="w-3 h-3 rounded-full bg-green-500/80"></span>
            <span class="ml-3 text-xs text-slate-500 font-mono">developer.ts</span>
          </div>
          <pre
            class="font-mono text-sm md:text-base leading-relaxed overflow-x-auto"
          ><code><span class="text-purple-400">const</span> <span class="text-blue-300">developer</span> = {
  <span class="text-sky-300">name</span>: <span class="text-emerald-400">'Kinn Beredico'</span>,
  <span class="text-sky-300">role</span>: <span class="text-emerald-400">'Full-Stack Developer'</span>,
  <span class="text-sky-300">focus</span>: <span class="text-emerald-400">'Performance & Reliability'</span>,
  <span class="text-sky-300">available</span>: <span class="text-orange-400">true</span>,
}</code></pre>
        </div>
        <div
          class="absolute -top-6 -right-6 glass rounded-2xl px-5 py-4 shadow-xl"
        >
          <p class="text-2xl font-black text-primary">{{ yearsExperience }}+</p>
          <p class="text-xs text-slate-400 font-semibold whitespace-nowrap">Years Experience</p>
        </div>
        <div class="absolute -top-10 -right-10 w-32 h-32 bg-primary/20 blur-3xl rounded-full -z-10"></div>
        <div
          class="absolute -bottom-10 -left-10 w-40 h-40 bg-blue-600/10 blur-3xl rounded-full -z-10"
        ></div>
      </div>
    </div>
  </section>

  <!-- Work history -->
  <WorkHistory />

  <!-- Skills -->
  <Skills />

  <!-- Projects -->
  <Projects />

  <!-- Services-->
  <Services />

  <!-- Contact-->
  <Contact />

  <!-- Footer -->
  <FooterSection />
</template>

<script setup lang="ts">
import Navbar from '@/components/Navbar.vue'
import WorkHistory from '@/components/WorkHistory.vue'
import Skills from '@/components/Skills.vue'
import Projects from '@/components/Projects.vue'
import Services from '@/components/Services.vue'
import Contact from '@/components/Contact.vue'
import FooterSection from '@/components/FooterSection.vue'

const yearsExperience = new Date().getFullYear() - 2019
</script>
