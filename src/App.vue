<script setup lang="ts">
import { ref, onMounted } from 'vue'
import BackgroundCanvas from './components/BackgroundCanvas.vue'
import HomeSection from './components/HomeSection.vue'
import AboutSection from './components/AboutSection.vue'
import SkillsSection from './components/SkillsSection.vue'
import WorkSection from './components/WorkSection.vue'
import ProjectsSection from './components/ProjectsSection.vue'
import ContactSection from './components/ContactSection.vue'

const showContent = ref(false)
const terminalLines = ref<string[]>([])
const skipped = ref(false)

const bootSequence = [
  { text: '> INITIALIZING SYSTEM...', delay: 500 },
  { text: '> LOADING CORE MODULES [####################] 100%', delay: 800 },
  { text: '> MOUNTING COMPONENTS...', delay: 400 },
  { text: '> ESTABLISHING SECURE CONNECTION...', delay: 600 },
  { text: '> ACCESS GRANTED.', delay: 400 },
  { text: '> WELCOME USER.', delay: 500 },
]

const runSequence = async () => {
  for (const step of bootSequence) {
    if (skipped.value) break
    terminalLines.value.push(step.text)
    await new Promise(resolve => setTimeout(resolve, step.delay))
  }
  finishBoot()
}

const finishBoot = () => {
  showContent.value = true
}

const skipAnimation = () => {
  skipped.value = true
  finishBoot()
}

onMounted(() => {
  runSequence()
})
</script>

<template>
  <div class="min-h-screen bg-primary text-gray-300 font-mono relative overflow-hidden selection:bg-accent selection:text-primary">
    <!-- Background Canvas (Always present) -->
    <BackgroundCanvas />

    <!-- Terminal Intro Overlay -->
    <transition name="fade">
      <div v-if="!showContent" class="fixed inset-0 z-50 flex items-center justify-center bg-primary p-4">
        <div class="max-w-2xl w-full space-y-2">
          <div v-for="(line, index) in terminalLines" :key="index" class="text-accent text-lg md:text-xl">
            {{ line }}
          </div>
          <div class="text-accent animate-pulse">_</div>
          
          <button @click="skipAnimation" 
                  class="fixed bottom-10 right-10 text-xs text-gray-600 hover:text-white border border-gray-800 hover:border-gray-500 px-3 py-1 rounded transition-colors uppercase">
            [Skip Intro]
          </button>
        </div>
      </div>
    </transition>

    <!-- Main Content -->
    <transition name="slide-up">
      <main v-if="showContent" class="relative z-10 w-full overflow-y-auto h-screen scroll-smooth">
        <!-- Navigation -->
        <nav class="flex justify-between items-center p-6 md:px-12 fixed top-0 w-full z-40 bg-gradient-to-b from-primary/95 to-transparent backdrop-blur-sm pointer-events-none transition-all duration-300">
          <div class="text-2xl font-bold text-accent pointer-events-auto cursor-pointer leading-none">
            dewansh<span class="text-white">.saboo</span>
          </div>
          
          <!-- Desktop Nav -->
          <div class="hidden md:flex space-x-8 text-sm pointer-events-auto font-mono">
            <a href="#about" class="hover:text-accent transition-colors"><span class="text-accent">01.</span> ABOUT</a>
            <a href="#skills" class="hover:text-accent transition-colors"><span class="text-accent">02.</span> SKILLS</a>
            <a href="#work" class="hover:text-accent transition-colors"><span class="text-accent">03.</span> WORK</a>
            <a href="#projects" class="hover:text-accent transition-colors"><span class="text-accent">04.</span> PROJECTS</a>
            <a href="#contact" class="hover:text-accent transition-colors"><span class="text-accent">05.</span> CONTACT</a>
          </div>

          <!-- Mobile Nav (Basic for now) -->
           <div class="md:hidden pointer-events-auto">
             <!-- Placeholder for mobile menu toggle -->
           </div>
        </nav>
        
        <!-- Right Side Email vertical (Optional, typical of this design style) -->
        <div class="hidden lg:flex fixed right-12 bottom-0 flex-col items-center gap-6 z-30 pointer-events-auto after:block after:w-px after:h-24 after:bg-gray-700 after:mt-6">
           <a href="mailto:dewanshsaboo28@gmail.com" class="vertical-writing text-sm text-gray-400 hover:text-accent hover:-translate-y-1 transition-all font-mono tracking-widest">
             dewanshsaboo28@gmail.com
           </a>
        </div>

         <!-- Left Side Socials vertical -->
        <div class="hidden lg:flex fixed left-12 bottom-0 flex-col items-center gap-6 z-30 pointer-events-auto after:block after:w-px after:h-24 after:bg-gray-700 after:mt-6">
           <a href="https://github.com/dewanshsaboo" target="_blank" class="text-gray-400 hover:text-accent hover:-translate-y-1 transition-all">
             <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M12 0c-6.626 0-12 5.373-12 12 0 5.302 3.438 9.8 8.207 11.387.599.111.793-.261.793-.577v-2.234c-3.338.726-4.033-1.416-4.033-1.416-.546-1.387-1.333-1.756-1.333-1.756-1.089-.745.083-.729.083-.729 1.205.084 1.839 1.237 1.839 1.237 1.07 1.834 2.807 1.304 3.492.997.107-.775.418-1.305.762-1.604-2.665-.305-5.467-1.334-5.467-5.931 0-1.311.469-2.381 1.236-3.221-.124-.303-.535-1.524.117-3.176 0 0 1.008-.322 3.301 1.23.957-.266 1.983-.399 3.003-.404 1.02.005 2.047.138 3.006.404 2.291-1.552 3.297-1.23 3.297-1.23.653 1.653.242 2.874.118 3.176.77.84 1.235 1.911 1.235 3.221 0 4.609-2.807 5.624-5.479 5.921.43.372.823 1.102.823 2.222v3.293c0 .319.192.694.801.576 4.765-1.589 8.199-6.086 8.199-11.386 0-6.627-5.373-12-12-12z"/></svg>
           </a>
           <a href="https://www.linkedin.com/in/dewansh-saboo-1323381ba/?originalSubdomain=in" target="_blank" class="text-gray-400 hover:text-accent hover:-translate-y-1 transition-all">
             <svg class="w-5 h-5" fill="currentColor" viewBox="0 0 24 24"><path d="M19 0h-14c-2.761 0-5 2.239-5 5v14c0 2.761 2.239 5 5 5h14c2.762 0 5-2.239 5-5v-14c0-2.761-2.238-5-5-5zm-11 19h-3v-11h3v11zm-1.5-12.268c-.966 0-1.75-.79-1.75-1.764s.784-1.764 1.75-1.764 1.75.79 1.75 1.764-.783 1.764-1.75 1.764zm13.5 12.268h-3v-5.604c0-3.368-4-3.113-4 0v5.604h-3v-11h3v1.765c1.396-2.586 7-2.777 7 2.476v6.759z"/></svg>
           </a>
        </div>

        <div class="px-6 md:px-24">
          <HomeSection />
          <AboutSection />
          <SkillsSection />
          <WorkSection />
          <ProjectsSection />
          <ContactSection />
          
          <footer class="text-center py-8 text-xs text-gray-600 relative z-10 font-mono">
            <p>DESIGNED & BUILT BY DEWANSH SABOO</p>
          </footer>
        </div>
      </main>
    </transition>
  </div>
</template>

<style scoped>
.vertical-writing {
  writing-mode: vertical-rl;
}

.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}

.slide-up-enter-active {
  transition: all 0.8s ease-out;
}

.slide-up-enter-from {
  opacity: 0;
  transform: translateY(20px);
}
</style>
