<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const props = defineProps<{
  text: string
}>()

const replay = () => {
    startScramble()
}

defineExpose({ replay })

const display = ref('')
const characters = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789!@#$%^&*()_+'
const target = ref<HTMLElement | null>(null)
let observer: IntersectionObserver | null = null

const startScramble = () => {
  let iterations = 0
  const interval = setInterval(() => {
    display.value = props.text
      .split('')
      .map((_, index) => {
        if (index < iterations) {
          return props.text[index]
        }
        return characters[Math.floor(Math.random() * characters.length)]
      })
      .join('')

    if (iterations >= props.text.length) {
      clearInterval(interval)
    }

    iterations += 1 / 3
  }, 30)
}

onMounted(() => {
  // Set initial random state
  display.value = props.text.split('').map(() => characters[Math.floor(Math.random() * characters.length)]).join('')
  
  observer = new IntersectionObserver((entries) => {
    if (entries[0]?.isIntersecting) {
      startScramble()
      if (observer && target.value) {
        observer.unobserve(target.value)
      }
    }
  })

  if (target.value) {
    observer.observe(target.value)
  }
})

onUnmounted(() => {
  if (observer) observer.disconnect()
})
</script>

<template>
  <span ref="target" class="font-mono inline-block">
    {{ display }}
  </span>
</template>
