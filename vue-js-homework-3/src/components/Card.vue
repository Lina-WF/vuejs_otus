<script setup>
import { ref } from 'vue'

defineProps({
  product: {
    id: Number,
    title: String,
    price: Number,
    description: String,
    category: String,
    image: String,
    rating: {
        rate: Number,
        count: Number,
    },
  },
});
</script>

<template>
  <div class="card">
    <img :src="product.image" :alt="'Изображение ' + product.title"/>
    <div class="info">
      <p>
        <big><b>{{ product.price }} $</b></big>
      </p>
      <p>
        <b>
          {{ product.title.length < 30 ? product.title : product.title.slice(0, 30) + "..." }}
        </b>
      </p>
      <p>
        ★ Рейтинг {{ product.rating.rate }} 
        <small>{{ product.rating.count }} оценок</small>
      </p>
      <p>
        {{ product.description.length < 90 ? product.description : product.description.slice(0, 90) + "..."}}
      </p>
      <p>
        <small :style="product.category === 'jewelery' ? 'margin-left: 2px' : '' ">
          {{ product.category }}
        </small>
      </p>
      <button>В корзину</button>
    </div>
  </div>
</template>

<style scoped>
.card {
  width: 25%;
  min-width: 300px;
  background-color: rgba(148, 117, 163, 0.331);
  border-radius: 15px;
  padding: 3%;
  margin: 1%;
}

img {
  max-height: 150px;
  width:auto;
  object-fit: contain;
}

.info {
    text-align: left;
    margin-left: 5%;
    margin-top: 10%;
}

small {
    color: rgb(186, 186, 186);
}

p {
    margin: 5px 0;
}

button {
    width: 100%;
    margin-top: 5px;
    margin-left: -2px;
}
</style>
