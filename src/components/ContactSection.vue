<script setup lang="ts">
import { ref } from 'vue'

const form = ref({
  name: '',
  email: '',
  message: ''
})

const submitForm = () => {
  console.log('Form submitted:', form.value)
  // Simulate submission or implement actual logic if needed
  alert('Thank you! I will get back to you soon.')
  form.value = { name: '', email: '', message: '' }
}

const socials = [
  { name: 'GitHub', url: 'https://github.com/dewanshsaboo', icon: 'github' }, // Assuming github handle based on name, can ask later
  { name: 'LinkedIn', url: 'https://www.linkedin.com/in/dewansh-saboo-1323381ba/?originalSubdomain=in', icon: 'linkedin' },
  { name: 'Email', url: 'mailto:dewanshsaboo28@gmail.com', icon: 'mail' }
]
</script>

<template>
  <section id="contact" class="min-h-screen flex items-center justify-center p-4 md:p-10 relative z-10 w-full max-w-7xl mx-auto">
    <!-- Big Curly Brace Left -->
    <div class="hidden lg:block text-[20rem] font-thin text-accent/20 leading-none select-none -translate-x-10">{</div>
    
    <div class="flex-1 w-full max-w-5xl bg-primary/80 backdrop-blur-sm border border-gray-800 p-8 rounded-lg shadow-2xl z-20">
      
      <div class="grid lg:grid-cols-2 gap-12">
        <!-- Left Column -->
        <div class="space-y-8">
          <div>
            <h2 class="text-4xl md:text-5xl font-bold mb-4">
              Have a project <span class="text-accent">in mind?</span>
            </h2>
            <p class="text-gray-400 text-lg">
              Let's create something awesome together. I'm always open to discussing new projects, creative ideas or opportunities to be part of your visions.
            </p>
          </div>

          <div class="flex flex-col space-y-4">
            <template v-for="social in socials" :key="social.name">
              <a :href="social.url" target="_blank" rel="noopener noreferrer" 
                 class="flex items-center gap-3 text-gray-400 hover:text-accent transition-colors group">
                <span class="p-2 border border-gray-700 rounded-md bg-white/5 group-hover:border-accent transition-colors">
                  <!-- Simple SVGs -->
                  <svg v-if="social.icon === 'github'" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
                  <svg v-if="social.icon === 'linkedin'" class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
                  <svg v-if="social.icon === 'mail'" class="w-5 h-5" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24"><path stroke-linecap="round" stroke-linejoin="round" d="M3 8l7.89 5.26a2 2 0 002.22 0L21 8M5 19h14a2 2 0 002-2V7a2 2 0 00-2-2H5a2 2 0 00-2 2v10a2 2 0 002 2z"/></svg>
                </span>
                <span class="font-mono">{{ social.name }}</span>
              </a>
            </template>
          </div>
        </div>

        <!-- Right Column - Form -->
        <form @submit.prevent="submitForm" class="space-y-6">
          <div class="grid md:grid-cols-2 gap-6">
            <div class="space-y-2">
              <label class="text-sm font-mono text-gray-500">NAME</label>
              <input v-model="form.name" type="text" required
                     class="w-full bg-transparent border-b border-gray-700 py-2 focus:outline-none focus:border-accent transition-colors font-mono placeholder-gray-700"
                     placeholder="John Doe" />
            </div>
            <div class="space-y-2">
              <label class="text-sm font-mono text-gray-500">EMAIL</label>
              <input v-model="form.email" type="email" required
                     class="w-full bg-transparent border-b border-gray-700 py-2 focus:outline-none focus:border-accent transition-colors font-mono placeholder-gray-700"
                     placeholder="john@example.com" />
            </div>
          </div>
          
          <div class="space-y-2">
            <label class="text-sm font-mono text-gray-500">MESSAGE</label>
            <textarea v-model="form.message" rows="4" required
                      class="w-full bg-transparent border-b border-gray-700 py-2 focus:outline-none focus:border-accent transition-colors font-mono placeholder-gray-700 resize-none"
                      placeholder="Hi, I'm interested in..." ></textarea>
          </div>

          <div class="flex justify-end pt-4">
            <button type="submit" 
                    class="bg-accent text-primary font-bold py-3 px-8 rounded hover:bg-opacity-90 transition-all hover:translate-x-1 font-mono uppercase tracking-wider">
              Submit &rarr;
            </button>
          </div>
        </form>
      </div>

    </div>

    <!-- Big Curly Brace Right -->
    <div class="hidden lg:block text-[20rem] font-thin text-accent/20 leading-none select-none translate-x-10">}</div>
  </section>
</template>
