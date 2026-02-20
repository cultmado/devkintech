<template>
  <section class="py-24">
    <div class="max-w-7xl mx-auto px-6">
      <div class="flex flex-col items-center mb-16">
        <span class="text-primary font-bold text-xs tracking-widest uppercase mb-2"
          >How I can help</span
        >
        <h2 class="text-4xl font-bold">Freelance Services</h2>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <div
          class="bg-charcoal p-10 rounded-3xl border border-slate-700 hover:border-primary/50 transition-colors"
        >
          <div
            class="w-16 h-16 bg-primary/10 rounded-2xl flex items-center justify-center text-primary mb-6"
          >
            <span class="material-symbols-outlined text-3xl">api</span>
          </div>
          <h3 class="text-2xl font-bold mb-4">API Development</h3>
          <p class="text-slate-400 leading-relaxed mb-6">
            Robust, secure, and scalable RESTful &amp; GraphQL APIs tailored for your front-end
            needs.
          </p>
          <ul class="space-y-3 text-sm text-slate-300">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Microservices Architecture
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span> Auth
              &amp; Security Protocols
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Documentation (Swagger)
            </li>
          </ul>
        </div>
        <div
          class="bg-primary p-10 rounded-3xl border border-primary/20 shadow-xl shadow-primary/20 text-white transform md:-translate-y-4"
        >
          <div
            class="w-16 h-16 bg-white/20 rounded-2xl flex items-center justify-center text-white mb-6"
          >
            <span class="material-symbols-outlined text-3xl">stay_primary_portrait</span>
          </div>
          <h3 class="text-2xl font-bold mb-4">Mobile App Design</h3>
          <p class="text-blue-100 leading-relaxed mb-6">
            Pixel-perfect cross-platform mobile apps using Flutter that run natively on iOS &amp;
            Android.
          </p>
          <ul class="space-y-3 text-sm text-blue-50">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> Native-feel
              performance
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> Push Notifications
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> App Store
              Submission
            </li>
          </ul>
        </div>
        <div
          class="bg-charcoal p-10 rounded-3xl border border-slate-700 hover:border-primary/50 transition-colors"
        >
          <div
            class="w-16 h-16 bg-primary/10 rounded-2xl flex items-center justify-center text-primary mb-6"
          >
            <span class="material-symbols-outlined text-3xl">laptop_mac</span>
          </div>
          <h3 class="text-2xl font-bold mb-4">Full-stack Web</h3>
          <p class="text-slate-400 leading-relaxed mb-6">
            Complete web ecosystems from interactive dashboards to complex e-commerce platforms.
          </p>
          <ul class="space-y-3 text-sm text-slate-300">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Responsive &amp; Accessible
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Database Optimization
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span> SEO
              Best Practices
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
