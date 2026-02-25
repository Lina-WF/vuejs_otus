<script setup>
import { computed, ref } from 'vue'
import ShopHeader from './components/ShopHeader.vue'
import Card from './components/Card.vue'
import Footer from './components/Footer.vue'
import BuyForm from './components/buyForm.vue';
import NewProductForm from './components/NewProductForm.vue';

const data = ref([]);

fetch("/products.json")
  .then((res) => res.json())
  .then((products) => data.value = products);

function checkProductInfo(info, searchTerm){
  const check = info.toLowerCase().includes(searchTerm.value.toLowerCase());
  return check;
}

function checkProductPrice(price, from, to){
  const check = from.value <= price && price <= to.value;
  return check;
}

const searchTerm = ref("");
const priceFrom = ref(0);
const priceTo = ref(1000000);
const filter = ref([searchTerm, priceFrom, priceTo]);

const products = computed(() => data.value.filter(product => (checkProductInfo(product.title, filter.value[0]) ||
                                                  checkProductInfo(product.description, filter.value[0]) ||
                                                  checkProductInfo(product.category, filter.value[0])) &&
                                                  checkProductPrice(product.price, filter.value[1], filter.value[2])));

const isNewProduct = ref(false);

const buyId = ref(-1);
const lastId = computed(() => data.value.length ? data.value.at(-1).id : 0);
</script>

<template>
  <ShopHeader @search="(e) => filter = e"/>
  <h1>Магазин</h1>
  <BuyForm :buyId="buyId" 
            @bought="() => buyId = -1"/>
  <NewProductForm :lastId="lastId"
                  :style="isNewProduct ? '' : 'display:none'"
                  @submited="(e) => {data.push(e); isNewProduct = false;}"/>
  <button style="width: 95%;"
          @click="isNewProduct = true">Добавить новый товар</button>
  <div v-if="products.length === 0">
    <div>
      <big>Товары по запросу не найдены.</big>
      <br>
      <br>
      Другие товары наши товары:
    </div>
    <div class="box">
      <Card v-for="product in data" 
          :key="product.id" 
          :product="product"
          @buy="(e) => buyId = e"
      />
    </div>
  </div>
  <div class="box" v-else>
    <Card v-for="product in products" 
          :key="product.id" 
          :product="product"
          @buy="(e) => buyId = e"
    />
  </div>
  <Footer />
</template>

<style scoped>
div{
  width: 100%;
}
.box {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
}
</style>
