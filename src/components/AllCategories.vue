<script setup lang="ts">
import MainCategory from './MainCategory.vue';
import json from '../test-json/properties.json'
</script>

<template>
    <div class="container">
        <div v-for="category in json.categories" :key="category.name">
            <MainCategory :Category="category"/>
        </div>
    </div>
</template>

<style scoped>

</style>
