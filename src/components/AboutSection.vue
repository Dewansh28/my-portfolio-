<script setup lang="ts">
import { ref } from 'vue'
import ScrambleText from './ScrambleText.vue'

const headingRef = ref<any>(null)
</script>

<template>
  <section id="about" class="min-h-screen flex items-center justify-center p-4 md:p-10 relative w-full max-w-7xl mx-auto">
    <!-- Big Curly Brace Left -->
    <div class="hidden lg:block text-[20rem] font-thin text-accent/20 leading-none select-none -translate-x-10">{</div>

    <div class="flex-1 w-full max-w-5xl bg-primary/80 backdrop-blur-sm border border-gray-800 p-8 rounded-lg z-20">
      <h2 class="text-3xl font-bold mb-8 flex items-center gap-4 cursor-default w-fit" @mouseenter="headingRef?.replay()">
        <span class="text-accent">01.</span> 
        <ScrambleText ref="headingRef" text="ABOUT ME" />
        <span class="h-px bg-gray-800 flex-1"></span>
      </h2>

      <div class="grid md:grid-cols-2 gap-12">
        <div class="space-y-6 text-gray-400 leading-relaxed font-mono md:col-span-2 lg:col-span-2">
          <p>
            Hi! I’m <span class="text-white">Dewansh</span>, a Computer Science graduate. I’m an <span class="text-accent">AI/ML Engineer</span> who loves building thoughtful digital experiences.
          </p>
          <p>
            I enjoy problem-solving with data and intelligent systems, while also crafting clean, intuitive web interfaces.
          </p>
          <p>
            Here are a few technologies I've been working with recently:
          </p>
          <ul class="grid grid-cols-2 sm:grid-cols-3 gap-2 text-sm">
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> JavaScript (ES6+)</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> TypeScript</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Vue 3</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Node.js</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Tailwind CSS</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Python</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Google Cloud</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> n8n</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> AI Agents</li>
            <li class="flex items-center gap-2"><span class="text-accent">▹</span> Machine Learning</li>
          </ul>
        </div>
      </div>
    </div>

    <!-- Big Curly Brace Right -->
    <div class="hidden lg:block text-[20rem] font-thin text-accent/20 leading-none select-none translate-x-10">}</div>
  </section>
</template>
