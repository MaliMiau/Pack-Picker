<script setup lang="ts">
import MainCategory from './MainCategory.vue';
import json from '../test-json/properties.json'
</script>

<template>
    <div class="container">
            <MainCategory v-for="category in json.categories" :key="category.name" :Category="category"/>
    </div>
</template>

<style scoped>
    .container {
        background-color: blue;
        width: fit-content;
        padding: 16px;
    }
</style>
