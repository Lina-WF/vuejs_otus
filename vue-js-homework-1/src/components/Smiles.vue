<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">Количество улыбнувшихся: {{ count }}</button>
  </div>
</template>

<style scoped>
button:hover {
  filter: drop-shadow(0 0 2em #903ac5c1);
}

button:active {
  filter: drop-shadow(0 0 2.5em #bd73ebc1);
}

@media (prefers-color-scheme: light) {
  button:active {
  filter: drop-shadow(0 0 2.5em #602187c1);
  }
}
</style>
