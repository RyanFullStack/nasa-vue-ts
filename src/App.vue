<script setup lang="ts">
import { ref } from 'vue'
import DailyPic from './components/DailyPic.vue'
import MarsPic from './components/MarsPics.vue'


const selectedComponent = ref<string>('dailypic')

interface Components {
  [key: string]: typeof DailyPic
}

const components: Components = {
  dailypic: DailyPic,
  marspics: MarsPic
}
</script>

<template>
  <select v-model="selectedComponent">
    <option value="dailypic">Daily Pic</option>
    <option value="marspics">Mars Pics</option>
  </select>
  <component :is="components[selectedComponent]" />
</template>
