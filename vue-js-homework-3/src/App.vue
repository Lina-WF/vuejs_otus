<script setup>
import { ref } from 'vue'
import ShopHeader from './components/ShopHeader.vue'
import Card from './components/Card.vue'
import Footer from './components/Footer.vue'

const data = ref();

fetch("/products.json")
  .then((res) => res.json())
  .then((products) => data.value = products);

</script>

<template>
  <ShopHeader />
  <h1>Магазин</h1>
  <div class="box">
    <Card v-for="product in data" :key="product.id" :product="product"/>
  </div>
  <Footer />
</template>

<style scoped>
.box {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>
