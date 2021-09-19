<script setup>
import Card from "./components/Card.vue";
import { onMounted, ref } from "@vue/runtime-core";
import axios from "axios";

const results = ref({});
const count = ref(1);

const handleNext = async () => {
  count.value++;
  await getData();
};

const handlePrev = async () => {
  count.value--;
  await getData();
};

const handleButton = async (e) => {
  const data = results.value.filter((el) => el.name.toLowerCase().includes(e.target.value));
  results.value = data.length > 0 ? data : results.value;
};
const getData = async () => {
  const { data } = await axios.get(`https://rickandmortyapi.com/api/character/?page=${count.value}`);
  results.value = data.results;
};

onMounted(async () => {
  await getData();
});
</script>

<template>
  <div class="fixed top-0 w-full z-40 bg-primary-900/50 backdrop-blur-md shadow-lg">
    <div class="container">
      <div class="flex flex-row justify-between items-center">
        <button @click="handlePrev" class="btn">PREV</button>
        <h4 class="text-white font-bold">Page {{ count }}</h4>
        <input type="text" v-model="count" @input="handleButton" />
        <button @click="handleButton" class="btn">IR</button>
        <button @click="handleNext" class="btn">NEXT</button>
      </div>
    </div>
  </div>
  <h1 class="font-bold text-5xl text-center text-white pt-6">Rick and Morty</h1>
  <div class="container my-8">
    <div class="grid grid-cols-1 md:grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-8">
      <Card :data="data" v-for="data in results" />
    </div>
  </div>
</template>

<style>
.btn {
  @apply bg-yellow-400 px-4 py-3 font-bold text-white;
}
</style>
