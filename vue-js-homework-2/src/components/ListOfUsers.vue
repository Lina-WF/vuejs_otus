<script setup>
import { ref } from 'vue'
import Hover from './Hover.vue'

const users = ref([
    {
        id: 0,
        name: "Иван",
        age: "28",
        job: "Тимлид"
    },
    {
        id: 1,
        name: "Дима",
        age: "23",
        job: "Бэкенд"
    },
    {
        id: 2,
        name: "Полина",
        age: "22",
        job: "Фронтенд"
    },
    {
        id: 3,
        name: "Мария",
        age: "25",
        job: "Датабаза"
    },
]);
</script>

<template>
    <ul>
        <li v-for="user in users">
            <Hover :obj="user" />
        </li>
    </ul>
</template>

<style scoped>
</style>
