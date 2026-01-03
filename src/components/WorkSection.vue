<script setup lang="ts">
import { ref } from 'vue'
import ScrambleText from './ScrambleText.vue'

const experiences = [
  {
    company: 'Osmos',
    role: 'AI / ML Engineer',
    range: 'Dec 2025 - Present',
    details: [
      'Designing and deploying end-to-end ML pipelines for business process optimization.',
      'Automating CRM workflows using n8n and AI-based enrichment to improve conversion insights.',
      'Building predictive models for hiring and lead conversion using Python, Scikit-Learn, and statistical methods.'
    ]
  },
  {
    company: 'Hummingbird',
    role: 'Business Analyst Intern',
    range: 'Mar 2025 - July 2025',
    details: [
      'Analyzed business requirements to drive data-driven decision making and process automation.',
      'Collaborated with cross-functional teams to optimize workflows and enhance product strategies.',
      'Leveraged data visualization tools to present actionable insights for stakeholder reporting.'
    ]
  }
]

const activeIndex = ref(0)
const headingRef = ref<any>(null)
</script>

<template>
  <section id="work" class="min-h-screen flex items-center justify-center p-4 py-20 w-full max-w-4xl mx-auto">
    <div class="w-full">
      <h2 class="text-3xl font-bold mb-12 flex items-center gap-4 cursor-default w-fit" @mouseenter="headingRef?.replay()">
        <span class="text-accent">03.</span> 
        <ScrambleText ref="headingRef" text="WORK EXPERIENCE" />
        <span class="h-px bg-gray-800 flex-1"></span>
      </h2>

      <div class="flex flex-col md:flex-row gap-8">
        <!-- Tab List -->
        <div class="flex md:flex-col overflow-x-auto md:overflow-visible border-b md:border-b-0 md:border-l border-gray-800 min-w-max">
          <button v-for="(exp, index) in experiences" :key="index"
                  @click="activeIndex = index"
                  class="px-6 py-3 text-left font-mono text-sm transition-all duration-300 border-b-2 md:border-b-0 md:border-l-2 hover:bg-accent/5 hover:text-accent whitespace-nowrap"
                  :class="activeIndex === index ? 'border-accent text-accent bg-accent/5' : 'border-transparent text-gray-500'">
            {{ exp.company }}
          </button>
        </div>

        <!-- Content -->
        <div class="flex-1 min-h-[300px]">
          <template v-for="(exp, index) in experiences" :key="index">
            <div v-if="activeIndex === index" class="animate-fade-in">
              <h3 class="text-xl font-bold text-gray-200">
                {{ exp.role }} <span class="text-accent">@ {{ exp.company }}</span>
              </h3>
              <p class="font-mono text-sm text-gray-500 mb-6 mt-1">{{ exp.range }}</p>
              
              <ul class="space-y-4">
                <li v-for="(detail, i) in exp.details" :key="i" class="flex gap-3 text-gray-400">
                  <span class="text-accent mt-1.5">▹</span>
                  <span>{{ detail }}</span>
                </li>
              </ul>
            </div>
          </template>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.animate-fade-in {
  animation: fadeIn 0.3s ease-out forwards;
}

@keyframes fadeIn {
  from { opacity: 0; transform: translateY(10px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
