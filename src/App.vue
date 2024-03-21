<script setup lang="ts">
import ref from 'vue'
import DailyPic from './components/DailyPic.vue'

const selectedComponent = ref<string>('dailypic')

const components = {
  dailypic: DailyPic
}
</script>

<template>
  <select v-model="selectedComponent">
    <option value="dailypic">Daily Pic</option>
    <option value="marspics">Mars Pics</option>
  </select>
  <component :is="components[SelectedComponent]" />
</template>
