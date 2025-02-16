<script setup lang="ts">
    import { ref } from 'vue';
    import MainCategory from './MainCategory.vue';
    import json from '../test-json/properties.json'
    const indexes:string[] = []

    json.versions.forEach(version => {
        indexes.push(version.id)
    });

    const current_version = ref(0)
    const update_version = (id: string) => {
        current_version.value = indexes.indexOf(id)
    }
</script>

<template>
    <div class="container">
        <div class="version-controller">
            <p v-for="version in json.versions" :key="version.id" @click="update_version(version.id)">  {{ version.id }}</p>
        </div>
        <MainCategory v-for="(category, index) in json.versions[current_version].categories" :key="category.name" :Category="category" :Index="index"/>
    </div>
</template>

<style scoped>
    .container {
        background-color: blue;
        width: fit-content;
        padding: 16px;
    }
    .version-controller {
        width: 100%;
        height: 48px;
        background: #000000bb;
        border: 0;
        border-radius: 16px;
        display: flex;
        flex-direction: row-reverse;
        color: white;
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-weight: 600;
        & p{
            &:not(:last-child):before{
                content: "/";
                margin-right: 16px;
            }
            margin-right: 16px;
            cursor: pointer;
        }
    }
</style>
