<script setup>
import { ref } from 'vue'
import Info from './Info.vue'

defineProps({
  obj: Object,
});

const hover = ref("");
const isVisible = ref(false);

function toggle() {
    isVisible.value = !isVisible.value;
}
</script>

<template>
    <p @mouseover="hover = 'highlight'" @mouseleave="hover = ''" :class="hover" @click="toggle">{{ obj.name }}</p>
    <Info :obj="obj" v-show="isVisible"/>
</template>

<style scoped>
.highlight {
    color: #b075d4;
    cursor: pointer;
}

@media (prefers-color-scheme: light) {
    .highlight {
    color: #571c7b;
    }
}
</style>
