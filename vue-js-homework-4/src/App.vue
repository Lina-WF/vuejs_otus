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
  const check = info.toLowerCase().includes(searchTerm.toLowerCase());
  return check;
}

function checkProductPrice(price, from, to){
  const check = from <= price && price <= to;
  return check;
}

const filter = ref({'searchTerm': "", 
                    'priceFrom': 0, 
                    'priceTo': 1000000});

const checkomg = computed(() => console.log(filter.value.searchTerm));
const products = computed(() => data.value.filter(product => (checkProductInfo(product.title, filter.value.searchTerm) ||
                                                  checkProductInfo(product.description, filter.value.searchTerm) ||
                                                  checkProductInfo(product.category, filter.value.searchTerm)) &&
                                                  checkProductPrice(product.price, filter.value.priceFrom, filter.value.priceTo)));

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
                  v-show="isNewProduct"
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
