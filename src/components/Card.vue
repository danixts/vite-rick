<script setup>
import Tilt from "./Tilt.vue"
import { ref } from "@vue/reactivity";

defineProps({
  data: Object,
});

const load = ref(false);

const lazy = () => {
  load.value = true;
};
</script>

<template>
  <Tilt>
    <div
      class="group flex flex-row justify-start items-center bg-gradient-to-br from-primary-700 to-primary-600 rounded-md hover:bg-primary-600/80 transition-all cursor-pointer hover:shadow-2xl shadow-xl relative"
    >
      <span class="absolute top-3 right-3 text-white/25 text-xs">{{ data.origin.name }}</span>
      <div
        v-if="!load"
        class="object-cover min-w-[180px] min-h-[180px] w-[180px] rounded-l-md bg-primary-900"
      ></div>
      <img
        :src="data.image"
        alt
        class="object-cover min-w-[180px] min-h-[180px] w-[180px] rounded-l-md transition-all duration-500"
        :class="!load ? 'opacity-0' : 'opacity-100'"
        v-show="load"
        @load="lazy"
      />
      <div class="px-8">
        <h3
          class="text-white font-bold text-center text-2xl group-hover:text-yellow-300 transition-colors"
        >{{ data.name }}</h3>
        <div class="flex flex-row space-x-2 items-center mt-2">
          <div
            class="shadow-lg rounded-full w-[10px] h-[10px]"
            :class="data.status === 'Alive' ? 'bg-gradient-to-br from-green-500 to-green-700' : 'bg-gradient-to-br from-red-500 to-red-700'"
          ></div>
          <span class="text-white/60 uppercase">{{ data.status }} - {{ data.species }}</span>
        </div>
      </div>
    </div>
  </Tilt>
</template>
