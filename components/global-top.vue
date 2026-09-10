<script setup lang="ts">
import { computed } from 'vue'
import { useNav } from '@slidev/client'

const { currentSlideNo, total, isPrintMode } = useNav()

const progress = computed(() => {
  if (total.value <= 0)
    return 0

  return Math.min(1, currentSlideNo.value / total.value)
})
</script>

<template>
  <div v-if="!isPrintMode" class="slide-progress" aria-hidden="true">
    <div class="slide-progress__track">
      <div
        class="slide-progress__value"
        :style="{ transform: `scaleX(${progress})` }"
      />
    </div>
  </div>
</template>

<style>
.slide-progress {
  position: fixed;
  inset: 0 0 auto;
  z-index: 1000;
  pointer-events: none;
}

.slide-progress__track {
  height: 3px;
  overflow: hidden;
  background: rgb(255 255 255 / 12%);
}

.slide-progress__value {
  width: 100%;
  height: 100%;
  transform-origin: left center;
  background: linear-gradient(90deg, #5ed4ff, #7df9c5);
  transition: transform 220ms ease;
}
</style>
