<script setup lang="ts">
import { ref } from 'vue'

interface PicData {
    title: string,
    date: string,
    url: string,
    explanation: string
}

const picData = ref<PicData>({title: '', date: '', url: '', explanation: ''})

async function getData() {
    const res = await fetch('https://api.nasa.gov/planetary/apod?api_key=DEMO_KEY')
    const data = await res.json()
    picData.value = data
}

getData()

</script>

<template>
    <h1>Pic Of The Day</h1>
    <div class="daily-pic-container">
    <h2>{{ picData.title }}</h2>
    {{ picData.date }}
    <img :src="picData.url" />
    <p>{{ picData.explanation }}</p>
    </div>
</template>

<style scoped>
.daily-pic-container {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 8px;
    max-width: 1600px;
    width: 100%;
}
img {
    max-width: 1600px;
    width: 90%;
}
p {
    max-width: 1400px;
}
</style>
