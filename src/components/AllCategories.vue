<script setup lang="ts">
    import { ref } from 'vue';
    import MainCategory from './MainCategory.vue';
    const props = defineProps({
        json:{
            type: Object,
            default:JSON.parse('{"versions": [{"id": "1.21", "categories":[{"name": "Category", "packs": [{"name":"Pack", "description":"Description"}]}]}]}'),
            required: true
        }
    })
    const indexes:string[] = []

    props.json?.versions.forEach((version: { id: string; }) => {
        indexes.push(version.id)
    });

    const current_version = ref(0)
    const update_version = (id: string) => {
        current_version.value = indexes.indexOf(id)
    }
    const emit = defineEmits(["updateSelected"])
    const updateSelected = (name:string, active:string, category:string) => {
        emit("updateSelected", name, active, category)
    }
</script>

<template>
    <div class="container">
        <div class="version-controller">
            <p v-for="version in json.versions" :key="version.id" @click="update_version(version.id)">  {{ version.id }}</p>
        </div>
        <MainCategory v-for="(category, index) in json.versions[current_version].categories" :key="category.name" :Category="category" :Index="index" @update-selected="(n, a, c) => updateSelected(n, a, c)"/>
    </div>
</template>

<style scoped>
    .container {
        background: #555;
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
