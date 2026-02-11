<script setup>
import { ref } from 'vue'
import ListOfUsers from './components/ListOfUsers.vue'

const isVisible = ref(false);
</script>

<template>
  <button @click="isVisible = !isVisible"><h1>{{ isVisible ? "Скрыть " : "Показать "}} участников проекта</h1></button>
  <ListOfUsers v-show="isVisible"/>
</template>

<style>
</style>
