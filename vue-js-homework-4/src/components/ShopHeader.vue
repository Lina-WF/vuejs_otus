<script setup>
import SearchBar from './SearchBar.vue'
</script>

<template>
<div class="header">
    <p class="logo">
        <a href="/">Logo</a>
    </p>
    <SearchBar @search="(e) => $emit('search', e)" />
    <p class="nav">
        <a href="/">Главная</a>
    </p>
</div>
</template>

<style scoped>
.header {
    width: 100%;
    display: flex;
    flex-wrap: wrap;
}
p {
    width: 20%;
    font-size: 1.3em;
}

.logo{
    text-align: left;
    padding-left: 5%;
}
.nav{
    text-align: right;
    padding-right: 5%;
}

@media (max-width: 785px) {
    .nav{
        padding-left: 10%;
        width: 10%;
    }
    .logo{
        display: none;
    }
}

</style>
