<script setup lang="ts">
import { ref } from 'vue'

interface PicData {
    title: string,
    date: string,
    hdurl: string,
    explanation: string
}

const picData = ref<PicData>({title: '', date: '', hdurl: '', explanation: ''})

async function getData() {
    const res = await fetch('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY')
    const data = await res.json()
    picData.value = data
}

getData()

</script>

<template>
    <h1>Nasa Pic of the Day</h1>
    <div class="daily-pic-container">
    {{ picData.date }}
    <img :src="picData.hdurl" />
    {{ picData.explanation }}
    </div>
</template>

<style scoped>
.daily-pic-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
}
img {
    max-width: 1600px;
}
</style>
