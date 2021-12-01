<script setup lang="ts">
import { ref } from 'vue'

const props = defineProps<{ name: string, isSpecial?: boolean }>()

const highlighted = ref(false)

const offsetX = (Math.random() - 0.5) * 100
const offsetY = (Math.random() - 0.5) * 100
const scale = 2 + Math.random() * 2

const style = {
  transform: `scale(${scale}) translate(${offsetX}%, ${offsetY}%)`
}

function onClick () {
  if (props.isSpecial) {
    highlighted.value = true
  }
}
</script>

<template>
  <img @click="onClick" class="creature" :src="`/images/${name}.gif`" :style="style" :class="{highlighted}">
</template>

<style scoped>
.creature {
  width: max(2.5vh, 2.5vw);
  image-rendering: pixelated;
}

.creature.highlighted {
  border: 5px solid goldenrod;
}
</style>
