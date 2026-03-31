<script setup lang="ts">
import { ref, onMounted, computed } from 'vue'
import { useLocale } from '@/composables/useLocale'
import TimelineItem from '@/components/ui/TimelineItem.vue'
import SectionHeading from '@/components/ui/SectionHeading.vue'
import type { Experience } from '@/types'

const { t } = useLocale()
const sectionRef = ref<HTMLElement | null>(null)

const items = computed<Experience[]>(() => t('experience.items') as unknown as Experience[])

onMounted(async () => {
  const { fadeInUp } = await import('@/composables/useAnimation')
  if (sectionRef.value) fadeInUp(sectionRef.value)
})
</script>

<template>
  <section id="experience" ref="sectionRef" class="app-section bg-bg">
    <div class="app-container">
      <SectionHeading number="01" :title="t('experience.title')" />

      <div class="w-full">
        <TimelineItem
          v-for="(item, index) in items"
          :key="item.company"
          :item="item"
          :force-expanded="index === 0"
        />
      </div>
    </div>
  </section>
</template>
