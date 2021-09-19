<template>
  <div class="fixed top-0 py-4 w-full z-40 bg-primary-900/50 backdrop-blur-md shadow-lg">
    <div class="container">
      <div class="flex flex-row justify-between items-center">
        <div class="flex items-center space-x-4">
          <input
            type="text"
            v-model="search"
            placeholder="Search..."
            class="bg-gray-100 rounded-md px-4 py-3 focus:ring-2 ring-yellow-400 focus:outline-none"
          />
          <!-- <button @click="handleButton" class="btn">IR</button> -->
        </div>
        <div class="flex flex-row space-x-4 items-center">
          <button @click="handlePrev" class="btn">Prev</button>
          <button @click="handleNext" class="btn">Next</button>
          <h4 class="text-white font-bold">Page {{ count }}</h4>
        </div>
      </div>
    </div>
  </div>
  <h1 class="font-bold text-5xl text-center text-white pt-[120px]">
    Rick and Morty -
    <b class="text-yellow-400">Vite</b>
  </h1>
  <div class="container my-8">
    <div class="grid grid-cols-1 md:grid-cols-1 lg:grid-cols-2 xl:grid-cols-3 gap-8">
      <Card
        :data="data"
        v-for="(data, index) in querySearch"
        :key="data.id"
        v-motion
        :delay="index * 50"
        :initial="{ opacity: 0 }"
        :enter="{ opacity: 1 }"
      />
    </div>

    <template v-if="querySearch.length === 0">
      <h1 class="text-center text-white/25 mt-32 w-full text-3xl">Data not found</h1>
    </template>
  </div>
</template>

<script setup>
import Card from "./components/Card.vue";
import { onMounted, ref, computed, reactive } from "vue";
import axios from "axios";

const results = reactive([]);
const count = ref(1);
const search = ref("");
const limit = ref(3)
const handleNext = async () => {
  /* if (count.value <= limit.value)  */count.value++
  await getData();
};

const handlePrev = async () => {
  count.value--;
  await getData();
};

const querySearch = computed(() => results.filter(({ name }) => name.toLowerCase().includes(search.value)));

const getData = async () => {
  const { data } = await axios.get(`https://rickandmortyapi.com/api/character/?page=${count.value}`);
  results.splice(0, results.length);
  /* if (count.value <= limit.value) */ results.push(...data.results);
};

onMounted(async () => {
  await getData();
});
</script>

<style>
.btn {
  @apply bg-yellow-400 px-4 py-3 font-bold text-white transition-all hover:bg-yellow-500 duration-500 rounded-md;
}
</style>
