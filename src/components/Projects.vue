<template>
  <section class="py-24 bg-charcoal/50" id="portfolio">
    <div class="max-w-7xl mx-auto px-6">
      <div class="text-center mb-16">
        <h2 class="text-4xl font-bold mb-4">Featured Projects</h2>
        <p class="text-slate-400">Selected work from my professional and personal collection.</p>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
        <div
          class="group glass rounded-2xl overflow-hidden hover:-translate-y-2 transition-all duration-300" v-for="project in projects"
        >
          <div
            class="h-56 bg-cover bg-center project_thumbnail"
            :style="{
              backgroundImage: `url(${project.image})`
            }"
          ></div>
          <div class="p-6">
            <div class="flex gap-2 mb-4">
              <span v-for="stack in project.stacks"
                class="text-[10px] uppercase font-black bg-primary/20 text-primary px-2 py-0.5 rounded"
                >{{stack}}</span
              >
            </div>
            <h3 class="text-xl font-bold mb-2">{{ project.name }}</h3>
            <p class="text-slate-400 text-sm mb-6 leading-relaxed">
              {{ project.description }}
            </p>
            <div class="flex items-center justify-between">
              <a
                class="text-primary font-bold text-sm flex items-center gap-1 hover:underline"
                :href="project.link"
                target="_blank"
                >Live Demo <span class="material-symbols-outlined text-base">open_in_new</span></a
              >
              <a
                v-if="project.mobile_app_link != null"
                class="text-primary font-bold text-sm flex items-center gap-1 hover:underline"
                :href="project.mobile_app_link"
                target="_blank"
                >Mobile App <span class="material-symbols-outlined text-base">open_in_new</span></a
              >
              <!-- <a class="text-slate-400 hover:text-white transition-colors" href="#"
                ><span class="material-symbols-outlined">code</span></a
              > -->
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const projects = ref([
  {
    image: 'assets/images/projects/Capex.png',
    name: 'CaPEx',
    description: 'TNVS - Web & Mobile App',
    stacks: ['Laravel', 'mysql', 'Flutter', 'linux'],
    link: 'https://capex.com.ph',
    mobile_app_link: null
  },
  {
    image: 'assets/images/projects/yachtiee.png',
    name: 'YACHTIEE',
    description: 'Exclusive perks and curated deals crafted for captains, crew, and explorers of the open sea. Unlock savings, luxury benefits, and unforgettable experiences wherever you go.',
    stacks: ['Laravel', 'mysql', 'linux', 'Ionic', 'Ionic Appflow'],
    link: 'https://yachtiee.ae/',
    mobile_app_link: null
  },
  {
    image: 'assets/images/projects/playnow-home-page.png',
    name: 'PlayNow',
    description: 'Sports Deal Platforms in the region of United Arab Emirates',
    stacks: ['Laravel', 'mysql', 'Ionic', 'ionic Appflow', 'linux'],
    link: 'https://playnow.ae',
    mobile_app_link: 'https://apps.apple.com/ph/app/playnow-active-lifestyle-app/id6753778471'
  },
  {
    image: 'assets/images/projects/recruit-system.png',
    name: 'PA Officer Admission Board Web Application',
    description: '',
    stacks: ['Laravel', 'livewire', 'mysql', 'linux'],
    link: 'https://recruit-system.og1pa.net/',
    mobile_app_link: null
  },
  {
    image: 'assets/images/projects/etbmac.png',
    name: 'eTBMAC',
    description: 'Electronic Tuberculosis Medical Advisory Committee',
    stacks: ['Laravel', 'mysql', 'linux'],
    link: 'https://etbmac.doh.gov.ph/login',
    mobile_app_link: null
  },
  {
    image: 'assets/images/projects/huptown.png',
    name: 'HUPTOWN',
    description: 'Travel App based in UK',
    stacks: ['Laravel', 'mysql', 'linux'],
    link: 'https://www.huptown.com',
    mobile_app_link: null
  },
])
</script>
