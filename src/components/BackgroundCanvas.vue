<script setup lang="ts">
import { onMounted, onUnmounted, ref } from 'vue'

const canvasRef = ref<HTMLCanvasElement | null>(null)

interface Point {
  x: number
  y: number
  age: number
  vx: number
  vy: number
}

const points = ref<Point[]>([])
const mouse = { x: 0, y: 0 }
let animationFrameId: number

const resizeCanvas = () => {
  if (canvasRef.value) {
    canvasRef.value.width = window.innerWidth
    canvasRef.value.height = window.innerHeight
  }
}

const addPoint = (x: number, y: number) => {
  // Add simplified "spark" points
  for (let i = 0; i < 2; i++) {
    points.value.push({
      x,
      y,
      age: 0,
       vx: (Math.random() - 0.5) * 2,
       vy: (Math.random() - 0.5) * 2
    })
  }
}

const update = () => {
  if (!canvasRef.value) return
  const ctx = canvasRef.value.getContext('2d')
  if (!ctx) return

  // Clear with fade effect for trails
  ctx.fillStyle = 'rgba(10, 10, 10, 0.2)'
  ctx.fillRect(0, 0, canvasRef.value.width, canvasRef.value.height)

  // Draw "DRAG ANYWHERE" text if idle? (Optional, maybe in CSS or separate)
  // For now just the sparks

  points.value.forEach((p, index) => {
    p.age++
    p.x += p.vx
    p.y += p.vy
    
    // Gravity/Friction
    p.vy += 0.05
    p.vx *= 0.99
    
    if (p.age > 50) {
      points.value.splice(index, 1)
    } else {
      ctx.fillStyle = `rgba(190, 242, 100, ${1 - p.age / 50})` // #bef264
      ctx.fillRect(p.x, p.y, 2, 2)
    }
  })

  animationFrameId = requestAnimationFrame(update)
}

const handleMouseMove = (e: MouseEvent) => {
  mouse.x = e.clientX
  mouse.y = e.clientY
  addPoint(mouse.x, mouse.y)
}

const handleTouchMove = (e: TouchEvent) => {
  const touch = e.touches[0]
  if (touch) {
    mouse.x = touch.clientX
    mouse.y = touch.clientY
    addPoint(mouse.x, mouse.y)
  }
}

onMounted(() => {
  window.addEventListener('resize', resizeCanvas)
  window.addEventListener('mousemove', handleMouseMove)
  window.addEventListener('touchmove', handleTouchMove)
  resizeCanvas()
  update()
})

onUnmounted(() => {
  window.removeEventListener('resize', resizeCanvas)
  window.removeEventListener('mousemove', handleMouseMove)
  window.removeEventListener('touchmove', handleTouchMove)
  cancelAnimationFrame(animationFrameId)
})
</script>

<template>
  <canvas 
    ref="canvasRef" 
    class="fixed top-0 left-0 w-full h-full pointer-events-none z-0"
  />
  <div class="fixed top-1/2 left-1/2 transform -translate-x-1/2 -translate-y-1/2 text-gray-800 text-6xl font-black opacity-10 pointer-events-none select-none z-0 whitespace-nowrap">
    DRAG ANYWHERE
  </div>
</template>
