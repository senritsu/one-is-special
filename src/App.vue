<script setup lang="ts">
import Chance from 'chance'

const chance = new Chance()

import Creature from './components/Creature.vue'

const names = Array.from({length: 30}).map((x, i) => `creature (${i})`)

const choices = chance.pickset(names, 13)

const [special, ...duplicates] = choices

const creatures = chance.shuffle([...duplicates, ...duplicates].map(name => ({name, isSpecial: false})).concat({name: special, isSpecial: true}))
</script>

<template>
  <div class="container">
    <Creature v-for="creature of creatures" v-bind="creature"></Creature>
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
  grid-template: repeat(5, 1fr) / repeat(5, 1fr);
  place-items: center;
  overflow: hidden;
}
</style>
