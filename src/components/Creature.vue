<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<{ name: string, isSpecial: boolean, disabled: boolean, highlighted: boolean, gameover: boolean }>()
const emit = defineEmits<{(name: 'click'): void}>()

const scale = 2 + Math.random() * 2
const offsetX = (Math.random() - 0.5) * (6 - scale) * 25
const offsetY = (Math.random() - 0.5) * (6 - scale) * 25

const style = computed(() => ({
  transform: `scale(${scale}) translate(${offsetX}%, ${offsetY}%)`,
  opacity: props.disabled ? 0.1 : 1,
  filter: props.gameover ? 'grayscale(1)' : null
}))
</script>

<template>
  <img @click="emit('click')" class="creature" :src="`/images/${name}.gif`" :style="style" :class="{highlighted}">
</template>

<style scoped>
.creature {
  width: max(2.5vh, 2.5vw);
  image-rendering: pixelated;
}

.creature.highlighted {
  animation: 1s ease infinite blink;
}

@keyframes blink {
    0% { filter: brightness(0.75) saturate(75%); }
    50% { 
      filter: 
        brightness(2) saturate(150%)
        drop-shadow(2px 2px 2px rgb(255, 217, 0))
        drop-shadow(-1px -1px 2px rgb(255, 217, 0))
        drop-shadow(1px -1px 2px rgb(255, 217, 0))
        drop-shadow(-1px 1px 2px rgb(255, 217, 0));
    }
    100% { filter: brightness(0.75) saturate(75%); }
}
</style>
