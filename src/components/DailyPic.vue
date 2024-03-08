<script setup lang="ts">
import { ref } from "vue";

interface PicData {
  title: string;
  date: string;
  url: string;
  explanation: string;
}

const picData = ref<PicData>({ title: "", date: "", url: "", explanation: "" });


function formatDate(date: Date) {
  const year = date.getFullYear();
  const month = String(date.getMonth() + 1).padStart(2, "0");
  const day = String(date.getDate()).padStart(2, "0");

  return `${year}-${month}-${day}`;
}
const today = new Date();
const chosenDate = ref<string>(formatDate(today));

async function getData(date: string) {
  const res = await fetch(
    `https://api.nasa.gov/planetary/apod?api_key=Xya2z9iHCUKGJvGqeSKRCyPDJWKcCuZkC8N8a3uk&date=${date}`
  );
  const data = await res.json();
  picData.value = data;
}

getData(formatDate(today));

function decrementDate() {
    const currentChoice = new Date(chosenDate.value)
    currentChoice.setDate(currentChoice.getDate())
    chosenDate.value = formatDate(currentChoice)
    getData(chosenDate.value)
}
</script>

<template>
  <div class="daily-pic-container">
    <h1>Pic Of The Day</h1>
    <div class="date-buttons">
      <button @click="decrementDate()">-1 Day</button>
      <button @click="getData(formatDate(today))">Today</button>
    </div>
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
.date-buttons {
  display: flex;
  gap: 5px;
}
img {
  max-width: 1600px;
  width: 90%;
}
p {
  max-width: 1400px;
}
</style>
