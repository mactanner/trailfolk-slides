<script setup lang="ts">
defineProps<{
  kind?: 'image' | 'diagram' | 'video'
  label: string
  h?: string
}>()

const labels = {
  image: 'Bild',
  diagram: 'Diagramm',
  video: 'Aufzeichnung',
}
</script>

<template>
  <div class="wm-placeholder" :style="{ height: h || '11rem' }">
    <div class="wm-placeholder__badge">{{ labels[kind || 'image'] }}</div>
    <div class="wm-placeholder__label">{{ label }}</div>
  </div>
</template>

<style scoped>
.wm-placeholder {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 0.6rem;
  padding: 1rem 1.4rem;
  border: 2px dashed rgb(0 164 224 / 40%);
  border-radius: 0.75rem;
  background: rgb(0 164 224 / 6%);
  text-align: center;
}

.wm-placeholder__badge {
  padding: 0.15rem 0.7rem;
  border-radius: 999px;
  background: rgb(0 164 224 / 18%);
  color: var(--css-blue-light);
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.14em;
  text-transform: uppercase;
}

.wm-placeholder__label {
  max-width: 46ch;
  font-size: 0.95rem;
  line-height: 1.35;
  opacity: 0.8;
}
</style>
