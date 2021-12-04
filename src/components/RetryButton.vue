<script setup lang="ts">
defineEmits<{(name: 'click'): void}>()
</script>

<template>
  <button class="retry" @click="$emit('click')">TRY AGAIN</button>
</template>

<style scoped>
.retry {
    font: 1.5em sans-serif;
    text-transform: uppercase;
    padding: 0.5em 2em;
    border: 8px solid #3b4153;
    border-radius: 5px;
    background-color: #131c24;
    color: whitesmoke;
    animation: 2s ease infinite shake;
}

@keyframes shake {
    0% {}
    75% { transform: rotate(0) }
    80% { transform: rotate(-2deg)}
    85% { transform: rotate(2deg)}
    90% { transform: rotate(-2deg)}
    95% { transform: rotate(2deg)}
    100% { transform: rotate(0) }
}
</style>