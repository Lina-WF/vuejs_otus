<script setup>
import { ref } from 'vue'
import ListOfUsers from './components/ListOfUsers.vue'

const isVisible = ref(false);

function toggle() {
    isVisible.value = !isVisible.value;
    console.log(isVisible.value);
    
}
</script>

<template>
  <button @click="toggle"><h1>{{ isVisible ? "Скрыть " : "Показать "}} участников проекта</h1></button>
  <ListOfUsers v-show="isVisible"/>
</template>

<style>
</style>
