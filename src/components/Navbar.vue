<template>
  <nav class="fixed top-6 left-0 right-0 z-50 flex justify-center px-4">
    <div
      class="glass flex items-center justify-between w-full max-w-5xl px-6 py-2.5 rounded-full shadow-2xl"
    >
      <div class="flex items-center gap-1 group cursor-pointer">
        <a href="#home">
          <span class="text-2xl font-black tracking-tighter text-white"
            >@devkintech<span class="text-primary">.</span></span
          >
        </a>
      </div>
      <div class="hidden md:flex items-center gap-8">
        <a
          class="nav-link text-xs font-bold uppercase tracking-widest text-slate-300 hover:text-white"
          href="#home"
          >Home</a
        >
        <a
          class="nav-link text-xs font-bold uppercase tracking-widest text-slate-300 hover:text-white"
          href="#experience"
          >Experiences</a
        >
        <a
          class="nav-link text-xs font-bold uppercase tracking-widest text-slate-300 hover:text-white"
          href="#skills"
          >Skills</a
        >
        <a
          class="nav-link text-xs font-bold uppercase tracking-widest text-slate-300 hover:text-white"
          href="#portfolio"
          >Portfolio</a
        >
        <a
          class="nav-link text-xs font-bold uppercase tracking-widest text-slate-300 hover:text-white"
          href="#contact"
          >Contact</a
        >
      </div>
      <div class="flex items-center">
        <a href="#contact"
          class="bg-gradient-to-r from-primary to-blue-600 hover:shadow-[0_0_20px_rgba(13,89,242,0.4)] text-white px-6 py-2 rounded-full text-xs font-black uppercase tracking-widest transition-all transform active:scale-95"
        >
          Hire Me
        </a>
      </div>
    </div>
  </nav>
</template>
