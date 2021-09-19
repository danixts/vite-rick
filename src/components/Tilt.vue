<template>
    <div :class="parallax ? 'preserve' : ''" ref="tilt">
        <slot></slot>
    </div>
</template>

<script setup>
import VanillaTilt from 'vanilla-tilt';
import { onMounted, ref, watchEffect } from 'vue';

defineProps({
    options: Object,
    parallax: Boolean
})

const tilt = ref(null)

onMounted(() => {
    VanillaTilt.init(tilt.value, { speed: 500, max: 16, glare: true })
})
</script>

<style>
.preserve {
    transform-style: preserve-3d;
}
</style>