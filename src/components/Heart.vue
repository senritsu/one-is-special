<script setup lang="ts">
defineProps<{ filled: boolean }>()
</script>

<template>
  <img class="heart" :src="`/images/heart_${filled ? 'filled' : 'empty'}.png`">
</template>

<style scoped>
.heart {
  margin: 0.5em;
  width: 3em;
  height: 3em;
  image-rendering: pixelated;
}
</style>
