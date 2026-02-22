<style scoped>
#profile-img {
  background-image: url('@/assets/images/mac.png')
}
</style>
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
          <span class="text-slate-100 font-bold">Full-Stack Developer</span> delivering scalable web and mobile applications with expertise in cloud infrastructure and deployment for high-performing, reliable systems.
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
            View Projects <span class="material-symbols-outlined">arrow_forward</span>
          </button>
          <button
            class="bg-charcoal hover:bg-slate-700 border border-slate-700 text-white px-8 py-4 rounded-xl font-bold transition-all"
          >
            Download CV
          </button>
        </div>
      </div>
      <div class="relative hidden lg:block">
        <div
          class="relative w-full aspect-square rounded-3xl overflow-hidden glass p-4 rotate-3 hover:rotate-0 transition-transform duration-500"
        >
          <div
            id="profile-img"
            class="w-full h-full bg-slate-800 rounded-2xl bg-cover bg-center shadow-2xl border border-slate-700"
          ></div>
        </div>
        <div class="absolute -top-6 -right-6 w-24 h-24 bg-primary/20 blur-3xl rounded-full"></div>
        <div
          class="absolute -bottom-10 -left-10 w-40 h-40 bg-blue-600/10 blur-3xl rounded-full"
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
import Navbar from '@/components/Navbar.vue';
import WorkHistory from '@/components/WorkHistory.vue';
import Skills from '@/components/Skills.vue';
import Projects from '@/components/Projects.vue';
import Services from '@/components/Services.vue';
import Contact from '@/components/Contact.vue';
import FooterSection from '@/components/FooterSection.vue';
</script>
