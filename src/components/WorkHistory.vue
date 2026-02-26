<template>
  <section class="py-24 bg-background-dark" id="experience">
    <div class="max-w-4xl mx-auto px-6">
      <div class="text-center mb-16">
        <h2 class="text-4xl font-bold mb-4">Professional History</h2>
        <div class="h-1 w-20 bg-primary mx-auto rounded-full"></div>
      </div>
      <div class="relative border-l-2 border-slate-800 ml-4 md:ml-0 space-y-12">
        <template v-for="(work, idx) in workHistory">
          <div class="relative pl-8 group">
            <div
              class="absolute -left-2.5 top-1.5 w-5 h-5 rounded-full bg-primary border-4 border-background-dark group-hover:scale-125 transition-transform"
            ></div>
            <div class="glass p-6 rounded-2xl group-hover:bg-slate-800/80 transition-all">
              <span class="text-primary text-sm font-bold">{{ work.length_of_service }}</span>
              <h3 class="text-xl font-bold mt-1">{{ work.job_title }}</h3>
              <p class="text-slate-400 font-medium mb-3">{{ work.company }}</p>
              <p class="text-slate-400 leading-relaxed">{{ work.description }}</p>
            </div>
          </div>
        </template>
        <!-- <div class="relative pl-8 group">
        <div
          class="absolute -left-2.5 top-1.5 w-5 h-5 rounded-full bg-slate-700 border-4 border-background-dark group-hover:bg-primary transition-colors"
        ></div>
        <div class="glass p-6 rounded-2xl group-hover:bg-slate-800/80 transition-all">
          <span class="text-slate-500 text-sm font-bold">2019 — 2021</span>
          <h3 class="text-xl font-bold mt-1">Mobile Developer</h3>
          <p class="text-slate-400 font-medium mb-3">Swiftly Apps Studio</p>
          <p class="text-slate-400 leading-relaxed">
            Developed 4+ production-ready Flutter applications for international clients in the
            Fintech and E-commerce sectors.
          </p>
        </div>
      </div> -->
        <!-- <div class="relative pl-8 group">
        <div
          class="absolute -left-2.5 top-1.5 w-5 h-5 rounded-full bg-slate-700 border-4 border-background-dark group-hover:bg-primary transition-colors"
        ></div>
        <div class="glass p-6 rounded-2xl group-hover:bg-slate-800/80 transition-all">
          <span class="text-slate-500 text-sm font-bold">2018 — 2019</span>
          <h3 class="text-xl font-bold mt-1">Software Engineer Intern</h3>
          <p class="text-slate-400 font-medium mb-3">DataFlow Corp</p>
          <p class="text-slate-400 leading-relaxed">
            Assisted in the migration of legacy monolith architectures to microservices using
            Node.js and Docker.
          </p>
        </div>
      </div> -->
      </div>
    </div>
  </section>
</template>

<script setup>
import { ref } from 'vue'

const workHistory = ref([
  {
    company: 'Vavasoftware Corporation',
    job_title: 'Backend Developer',
    length_of_service: 'Jun 2023 - Present',
    description:
      'As a Backend Developer at Vavasoftware Corporation, I develop REST APIs using Laravel, build web applications with Vue.js, integrate third-party APIs, manage AWS cloud servers, and implement CI/CD pipelines using GitLab.',
  },
  {
    company: 'Philippine Army',
    job_title: 'Computer Programmer',
    length_of_service: 'May 2022 - Jun 2023',
    description:
      'As a Computer Programmer in the Philippine Army, I developed internal web-based systems and managed servers to support organizational operations.',
  },
  {
    company: 'ThinkBIT Solutions',
    job_title: 'Backend Developer',
    length_of_service: 'Oct 2021 - Apr 2022',
    description:
      'As a Backend Developer at ThinkBIT Solutions, I developed REST APIs using Laravel, performed database normalization, and integrated Stripe payment gateway.',
  },
  {
    company: 'Cargo Padala Express',
    job_title: 'Software Developer',
    length_of_service: 'Sept 2020 - Oct 2021',
    description:
      'As a Software Developer at Cargo Padala Express, I developed REST APIs using Laravel, built a mobile application with Flutter, integrated PayMongo payment gateway, performed database normalization, implemented UI/UX designs, and handled third-party API integrations.',
  },
  {
    company: 'Eclectus Technologies Inc.',
    job_title: 'Junior Software Developer',
    length_of_service: 'May 2019 - Oct 2021',
    description:
      'As a Junior Software Developer at Eclectus Technologies Inc., I performed manual software testing, created user manuals, developed mobile applications using Ionic Framework, built REST APIs with ASP.NET Core, and integrated third-party APIs.',
  },
])
</script>
