<script setup lang="ts">
import { ref, onMounted } from 'vue'

const roles = ['FULL STACK DEVELOPER', 'AI / ML ENGINEER', 'WEB DEVELOPMENT ENTHUSIAST']
const currentRole = ref('')
const roleIndex = ref(0)
const charIndex = ref(0)
const isDeleting = ref(false)

const typeRole = () => {
  const role = roles[roleIndex.value]
  if (!role) return
  
  if (isDeleting.value) {
    currentRole.value = role.substring(0, charIndex.value - 1)
    charIndex.value--
  } else {
    currentRole.value = role.substring(0, charIndex.value + 1)
    charIndex.value++
  }

  if (!isDeleting.value && charIndex.value === role.length) {
    setTimeout(() => isDeleting.value = true, 2000)
    setTimeout(typeRole, 2000)
  } else if (isDeleting.value && charIndex.value === 0) {
    isDeleting.value = false
    roleIndex.value = (roleIndex.value + 1) % roles.length
    setTimeout(typeRole, 500)
  } else {
    const speed = isDeleting.value ? 50 : 100
    setTimeout(typeRole, speed)
  }
}

onMounted(() => {
  typeRole()
})
</script>

<template>
  <section id="home" class="min-h-screen flex items-center justify-center relative p-4">
    <div class="text-center space-y-6 z-10 max-w-4xl">
      <h2 class="text-gray-400 text-lg md:text-xl font-mono">HELLO, WORLD! I'M</h2>
      <h1 class="text-6xl md:text-8xl font-bold tracking-tighter text-white glitch-text" data-text="DEWANSH SABOO">
        DEWANSH SABOO
      </h1>
      
      <div class="h-8 md:h-12 flex items-center justify-center">
        <span class="text-accent text-xl md:text-3xl font-mono font-bold">
          > {{ currentRole }}<span class="animate-pulse">_</span>
        </span>
      </div>

      <div class="flex gap-6 justify-center pt-8">
        <a href="#contact" 
           class="bg-accent text-primary font-bold py-3 px-8 rounded hover:bg-opacity-90 transition-all hover:translate-x-1 font-mono">
          CONTACT ME
        </a>
        <a href="#about" 
           class="border border-gray-600 text-gray-300 py-3 px-8 rounded hover:border-accent hover:text-accent transition-all font-mono group flex items-center gap-2">
          LEARN MORE
          <span class="group-hover:rotate-90 transition-transform duration-300">↓</span>
        </a>
      </div>
    </div>
  </section>
</template>

<style scoped>
.glitch-text {
  position: relative;
}
</style>
