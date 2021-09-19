<script setup>
defineProps({
  data: Object,
});
</script>

<template>
  <div
    class="
      group
      flex flex-row
      justify-start
      items-center
      bg-gradient-to-br
      from-primary-700
      to-primary-600
      rounded-md
      hover:bg-primary-600/80
      transition-all
      cursor-pointer
      hover:scale-105 hover:shadow-2xl
      shadow-xl
      relative
    "
  >
    <span class="absolute top-3 right-3 text-white/25 text-xs">{{ data.origin.name }}</span>
    <img :src="data.image" alt="" class="object-cover w-[180px] rounded-l-md" />
    <div class="px-8">
      <h3 class="text-white font-bold text-center text-2xl group-hover:text-yellow-300 transition-colors">{{
        data.name
      }}</h3>
      <div class="flex flex-row space-x-2 items-center mt-2">
        <div
          class="rounded-full w-[8px] h-[8px]"
          :class="data.status === 'Alive' ? 'bg-green-500' : 'bg-red-500'"
        ></div>
        <span class="text-white/60 uppercase">{{ data.status }} - {{ data.species }}</span>
      </div>
    </div>
  </div>
</template>
