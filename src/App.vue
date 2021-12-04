<script setup lang="ts">
import {ref} from 'vue'
import Chance from 'chance'

const chance = new Chance()

import Creature from './components/Creature.vue'
import Heart from './components/Heart.vue'
import RetryButton from './components/RetryButton.vue'

const names = Array.from({length: 40}).map((x, i) => `creature (${i})`)

const creatures = ref([] as {name: string, isSpecial: boolean}[])
const hearts = ref(0)
const mistakes = ref([] as string[])
const found = ref(false)
const attempt = ref(0)

function onClick (i: number) {
  if (!hearts.value || found.value) return

  const creature = creatures.value[i]

  console.log(creature)

  if (creature.isSpecial) {
    found.value = true
  } else if (!mistakes.value.includes(creature.name)) {
    mistakes.value.push(creature.name)
    hearts.value -= 1
  }

  console.log(mistakes.value)
}

function reset () {
  const [special, ...duplicates] = chance.pickset(names, 13)

  creatures.value = chance.shuffle([...duplicates, ...duplicates].map(name => ({name, isSpecial: false})).concat({name: special, isSpecial: true}))
  hearts.value = 3
  mistakes.value = []
  found.value = false
  attempt.value += 1
}

reset()
</script>

<template>
  <div class="container">
    <header class="header">
      <h1 class="text" v-if="hearts && !found">One is special! Can you find it?</h1>
      <RetryButton v-else @click="reset" />
    </header>
    <Creature v-for="(creature, i) of creatures" :key="`${attempt}-${i}`" v-bind="creature" :disabled="mistakes.includes(creature.name)" :highlighted="found && creature.isSpecial" @click="onClick(i)"></Creature>
    <div class="hearts">
      <Heart v-for="i in 3" :filled="i <= hearts" />
    </div>
  </div>
</template>

<style>
body {
  margin: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: #131c24;

  width: 100vw;
  height: 100vh;
}

.container {
  display: grid;
  width: 100%;
  height: 100%;
  grid-template: 5em repeat(5, 1fr) auto / repeat(5, 1fr);
  place-items: center;
  overflow: hidden;
}

.hearts, .header {
  grid-column: span 5;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0.5em;
}

.text {
  font: 2em sans-serif;
}
</style>
