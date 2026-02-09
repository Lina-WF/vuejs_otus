<script setup>
import { ref } from 'vue'

defineProps({
  obj: Object,
});
</script>

<template>
    <ul>
        <li><p>Возраст: {{ obj.age }}</p></li>
        <li><p>Позиция: {{ obj.job }}</p></li>
    </ul>
</template>

<style scoped>
ul {
    background-color: #571c7b75;
    padding: 1px 15px;
    border-radius: 10px;
}

@media (prefers-color-scheme: light) {
    ul {
        background-color: #b075d4;;
    }
}
</style>
