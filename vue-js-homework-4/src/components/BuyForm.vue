<script setup>
import { computed, ref } from 'vue';
import DeliveryForm from './DeliveryForm.vue';
import CardForm from './CardForm.vue';

const prop = defineProps({buyId: Number});
const emit = defineEmits('bought');

const id = computed(() => prop.buyId);
const deliveryRes = ref();
const cardRes = ref();
const response = ref("Ожидание ответа");

async function postForm(delivery, card){
    let data = JSON.stringify(Object.assign(delivery, card), null, 2);
    let res = await fetch('https://httpbin.org/post', {
        method: 'POST',
        headers: {
            'Content-Type': 'application/json' 
        },
        body: data
        });
    if (res.ok) {
        response.value = "Оплата прошла успешно";
    }
    else{
        response.value = "Что-то пошло не так";
    }
}

function close(){
    cardRes.value = "";
    deliveryRes.value = "";
    response.value = ref("Ожидание ответа");
    emit('bought');
}
</script>

<template> 
<DeliveryForm class="glass"
                v-show="!(buyId === -1 || deliveryRes)"
                :buyId="id" 
                @submited="(e) => deliveryRes = e" />
<CardForm class="glass"
            v-show="deliveryRes && !cardRes"
            @submited="(e) => {cardRes = e; postForm(deliveryRes, e)}" />
<div class="glass"
    :style="cardRes ? '' :  'display:none'" >
    <big><b>{{ response }}</b></big><br><br>
    <button @click="close">Закрыть</button>
</div>
</template>

<style scoped>
</style>
