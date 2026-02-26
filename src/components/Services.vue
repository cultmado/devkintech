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
            I design and build secure, scalable, and high-performance RESTful APIs to power web and mobile applications. My APIs follow best practices in architecture, authentication, and documentation to ensure reliability and easy integration.
          </p>
          <ul class="space-y-3 text-sm text-slate-300">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Microservices-ready architecture
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span> Secure authentication (JWT, OAuth, Sanctum, etc.)
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Well-documented APIs
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Database optimization & performance tuning
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
          <h3 class="text-2xl font-bold mb-4">Mobile App Development</h3>
          <p class="text-blue-100 leading-relaxed mb-6">
            I develop fast, modern cross-platform mobile applications, delivering smooth performance and native-like user experiences on Android and iOS.
          </p>
          <ul class="space-y-3 text-sm text-blue-50">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> Cross-platform Android & iOS apps
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> Clean UI/UX with responsive design
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> Push notifications & third-party API integration
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-lg">check_circle</span> App Store & Play Store deployment support
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
          <h3 class="text-2xl font-bold mb-4">Full-Stack Web Development</h3>
          <p class="text-slate-400 leading-relaxed mb-6">
            I build complete web applications from backend to frontend, focusing on performance, security, and user experience. From dashboards to e-commerce platforms, I deliver scalable solutions tailored to business needs.
          </p>
          <ul class="space-y-3 text-sm text-slate-300">
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>Modern frontend design
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span>
              Database Optimization
            </li>
            <li class="flex items-center gap-2">
              <span class="material-symbols-outlined text-primary text-lg">check_circle</span> SEO-friendly and responsive UI
            </li>
          </ul>
        </div>
      </div>
    </div>
  </section>
</template>
