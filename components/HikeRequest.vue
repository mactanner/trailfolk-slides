<script setup lang="ts">
defineProps<{
  compact?: boolean
}>()
</script>

<template>
  <div class="hike-request" :class="{ 'hike-request--compact': compact }">
    <p class="hike-request__message">
      <span>Ich suche eine <strong>anspruchsvolle Wanderung</strong></span>
      <span>im <strong>Berner Oberland</strong> - rund <strong>15 km</strong></span>
      <span>und mindestens <strong>1200 Meter Aufstieg</strong>.</span>
    </p>
  </div>
</template>

<style scoped>
.hike-request {
  position: relative;
  padding: 2rem 2.25rem;
  border-radius: 1.5rem 1.5rem 1.5rem 0.35rem;
  background: rgb(255 255 255 / 6%);
  text-align: left;
}

.hike-request::after {
  position: absolute;
  bottom: -1rem;
  left: 0;
  width: 1.25rem;
  height: 1rem;
  background: rgb(255 255 255 / 6%);
  clip-path: polygon(0 0, 100% 0, 0 100%);
  content: "";
}

.hike-request__message {
  margin: 0;
  font-size: 2rem;
  font-weight: 400;
  line-height: 1.5;
}

.hike-request__message > span {
  display: block;
}

.hike-request__message strong {
  color: var(--css-blue-light);
  font-weight: 650;
}

.hike-request--compact {
  padding: 1.25rem 1.75rem;
}

.hike-request--compact .hike-request__message {
  font-size: 1.625rem;
  line-height: 1.45;
}
</style>
