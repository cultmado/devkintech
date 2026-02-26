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
                <p class="text-lg font-bold">kinnberedico.work@gmail.com</p>
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
        <form class="space-y-6">
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <div class="space-y-2">
              <label class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
                >Full Name</label
              >
              <input
                class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none"
                placeholder="Enter your name"
                type="text"
              />
            </div>
            <div class="space-y-2">
              <label class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
                >Email Address</label
              >
              <input
                class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none"
                placeholder="Enter your email address"
                type="email"
              />
            </div>
          </div>
          <div class="space-y-2">
            <label class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
              >Subject</label
            >
            <select
              class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none appearance-none"
            >
              <option>Freelance Project</option>
              <option>Job Opportunity</option>
              <option>Technical Consultation</option>
              <option>Just Saying Hi</option>
            </select>
          </div>
          <div class="space-y-2">
            <label class="text-xs font-bold uppercase tracking-widest text-slate-500 px-1"
              >Message</label
            >
            <textarea
              class="w-full bg-slate-800/50 border-slate-700 rounded-xl px-4 py-4 focus:ring-2 focus:ring-primary focus:border-transparent transition-all outline-none resize-none"
              placeholder="Tell me about your vision..."
              rows="4"
            ></textarea>
          </div>
          <button
            class="w-full bg-primary hover:bg-primary/90 text-white font-bold py-5 rounded-xl transition-all shadow-lg shadow-primary/20 flex items-center justify-center gap-2 group"
          >
            Send Message
            <span class="material-symbols-outlined group-hover:translate-x-1 transition-transform"
              >send</span
            >
          </button>
        </form>
      </div>
    </div>
  </section>
</template>
