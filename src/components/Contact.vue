<template>
  <section class="py-24 bg-background-dark relative" id="contact">
    <div class="max-w-7xl mx-auto px-6">
      <div
        class="glass rounded-[40px] p-8 md:p-16 grid grid-cols-1 lg:grid-cols-2 gap-16 items-start"
      >
        <div>
          <h2 class="text-5xl font-black mb-6">
            Let's build something <span class="text-primary">extraordinary.</span>
          </h2>
          <p class="text-slate-400 text-lg leading-relaxed mb-10">
            Whether you have a specific project in mind or just want to explore possibilities, I'm
            always open to discussing new opportunities.
          </p>
          <div class="space-y-6">
            <div class="flex items-center gap-4 group">
              <div
                class="w-12 h-12 bg-slate-800 rounded-xl flex items-center justify-center text-primary group-hover:bg-primary group-hover:text-white transition-all"
              >
                <span class="material-symbols-outlined">mail</span>
              </div>
              <div>
                <p class="text-xs text-slate-500 font-bold uppercase tracking-widest">Email me</p>
                <a
                  :href="`mailto:${EMAIL}`"
                  class="text-lg font-bold hover:text-primary transition-colors"
                  >{{ EMAIL }}</a
                >
              </div>
            </div>
            <div class="flex items-center gap-4 group">
              <div
                class="w-12 h-12 bg-slate-800 rounded-xl flex items-center justify-center text-primary group-hover:bg-primary group-hover:text-white transition-all"
              >
                <span class="material-symbols-outlined">call</span>
              </div>
              <div>
                <p class="text-xs text-slate-500 font-bold uppercase tracking-widest">Call me</p>
                <a
                  href="tel:+639063454364"
                  class="text-lg font-bold hover:text-primary transition-colors"
                  >(0906) 345 4364</a
                >
              </div>
            </div>
            <div class="flex items-center gap-4 group hidden">
              <div
                class="w-12 h-12 bg-slate-800 rounded-xl flex items-center justify-center text-primary group-hover:bg-primary group-hover:text-white transition-all"
              >
                <span class="material-symbols-outlined">chat</span>
              </div>
              <div>
                <p class="text-xs text-slate-500 font-bold uppercase tracking-widest">
                  Social Presence
                </p>
                <div class="flex gap-4 mt-1">
                  <a class="text-slate-400 hover:text-white transition-colors font-bold" href="#"
                    >GitHub</a
                  >
                  <span class="text-slate-700">•</span>
                  <a class="text-slate-400 hover:text-white transition-colors font-bold" href="#"
                    >LinkedIn</a
                  >
                  <span class="text-slate-700">•</span>
                  <a class="text-slate-400 hover:text-white transition-colors font-bold" href="#"
                    >Twitter</a
                  >
                </div>
              </div>
            </div>
          </div>
        </div>
        <form class="space-y-6" @submit.prevent="submit">
          <!-- honeypot: bots fill it, humans never see it -->
          <input
            v-model="botcheck"
            type="checkbox"
            name="botcheck"
            class="hidden"
            tabindex="-1"
            autocomplete="off"
          />
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="space-y-2">
              <label
                for="contact-name"
                class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
                >Full Name</label
              >
              <input
                id="contact-name"
                v-model.trim="form.name"
                class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none"
                placeholder="Enter your name"
                type="text"
                name="name"
                autocomplete="name"
                maxlength="100"
                required
              />
            </div>
            <div class="space-y-2">
              <label
                for="contact-email"
                class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
                >Email Address</label
              >
              <input
                id="contact-email"
                v-model.trim="form.email"
                class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none"
                placeholder="Enter your email address"
                type="email"
                name="email"
                autocomplete="email"
                maxlength="254"
                required
              />
            </div>
          </div>
          <div class="space-y-2">
            <label
              for="contact-subject"
              class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
              >Subject</label
            >
            <select
              id="contact-subject"
              v-model="form.subject"
              class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none appearance-none"
              name="subject"
              required
            >
              <option v-for="subject in subjects" :key="subject">{{ subject }}</option>
            </select>
          </div>
          <div class="space-y-2">
            <label
              for="contact-message"
              class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
              >Message</label
            >
            <textarea
              id="contact-message"
              v-model.trim="form.message"
              class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none resize-none"
              placeholder="Tell me about your vision..."
              name="message"
              rows="4"
              maxlength="5000"
              required
            ></textarea>
          </div>
          <button
            type="submit"
            :disabled="status === 'sending'"
            class="w-full bg-primary hover:bg-primary/90 disabled:opacity-60 disabled:cursor-not-allowed text-white font-bold py-5 rounded-xl transition-all shadow-lg shadow-primary/20 flex items-center justify-center gap-2 group"
          >
            {{ status === 'sending' ? 'Sending…' : 'Send Message' }}
            <span class="material-symbols-outlined group-hover:translate-x-1 transition-transform"
              >send</span
            >
          </button>
          <div aria-live="polite">
            <p
              v-if="status === 'success'"
              class="rounded-xl border border-emerald-500/30 bg-emerald-500/10 px-4 py-3 text-emerald-300 font-semibold"
            >
              Thanks! Your message is on its way — I'll get back to you soon.
            </p>
            <p
              v-else-if="status === 'error'"
              class="rounded-xl border border-red-500/30 bg-red-500/10 px-4 py-3 text-red-300 font-semibold"
            >
              Sorry, your message couldn't be sent.
              <a :href="mailtoLink" class="underline hover:text-white">Email me directly</a>
              — your message will be pre-filled.
            </p>
          </div>
        </form>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed, reactive, ref } from 'vue'

const EMAIL = 'kinnberedico.work@gmail.com'
const WEB3FORMS_KEY = import.meta.env.VITE_WEB3FORMS_KEY

const subjects = [
  'Freelance Project',
  'Job Opportunity',
  'Technical Consultation',
  'Just Saying Hi',
]

const form = reactive({ name: '', email: '', subject: subjects[0], message: '' })
const botcheck = ref(false)
const status = ref<'idle' | 'sending' | 'success' | 'error'>('idle')

// fallback for when sending fails, so visitors don't lose what they typed
const mailtoLink = computed(
  () =>
    `mailto:${EMAIL}?subject=${encodeURIComponent(`${form.subject} — ${form.name}`)}` +
    `&body=${encodeURIComponent(form.message)}`,
)

async function submit() {
  if (status.value === 'sending') return

  if (!WEB3FORMS_KEY) {
    console.error('VITE_WEB3FORMS_KEY is not set')
    status.value = 'error'
    return
  }

  status.value = 'sending'
  try {
    const res = await fetch('https://api.web3forms.com/submit', {
      method: 'POST',
      headers: { 'Content-Type': 'application/json', Accept: 'application/json' },
      body: JSON.stringify({
        access_key: WEB3FORMS_KEY,
        subject: `[Portfolio] ${form.subject} — ${form.name}`,
        from_name: 'devkintech portfolio',
        name: form.name,
        email: form.email,
        topic: form.subject,
        message: form.message,
        botcheck: botcheck.value,
      }),
    })
    const data = await res.json()
    if (!res.ok || !data.success) throw new Error(data.message ?? `HTTP ${res.status}`)

    status.value = 'success'
    Object.assign(form, { name: '', email: '', subject: subjects[0], message: '' })
  } catch (err) {
    console.error('Contact form failed:', err)
    status.value = 'error'
  }
}
</script>
