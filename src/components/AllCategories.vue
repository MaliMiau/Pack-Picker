<script setup lang="ts">
    import { ref } from 'vue';
    import MainCategory from './MainCategory.vue';
    const props = defineProps({
        json:{
            type: Object,
            default: () => ({"versions": [{"id": "version", "categories":[{"name": "Category", "packs": [{"name":"Pack", "description":"Description"}]}]}]}),
            required: true
        },
        Incompatibilities:{
            type: Array,
            required: true
        },
        jsonIncompatibilities:{
            type: Object,
            default: () => ({"a": [""]})
        }
    })
    const indexes:string[] = []

    props.json.versions.forEach((version: { id: string; }) => {
        indexes.push(version.id)
    });

    const emit = defineEmits(["updateVersion", "updateSelected"])
    const current_version = ref(0)
    const update_version = (id: string) => {
        current_version.value = indexes.indexOf(id)
        emit('updateVersion', indexes.indexOf(id))
    }
</script>

<template>
    <div class="container">
        <div class="version-controller">
            <p v-for="version in json.versions" :key="version.id" @click="update_version(version.id)">  
                {{ version.id }}
            </p>
        </div>
        
        <MainCategory 
            v-for="(category, index) in json.versions[current_version].categories" 
            :key="category.name" 
            :Category="category" 
            :Index="index" 
            :Incompatibilities="Incompatibilities"
            :jsonIncompatibilities="jsonIncompatibilities"
            @update-selected="(n, a, c) => $emit('updateSelected', n, a, c)"
        />
    </div>
</template>

<style scoped>
    .container {
        background: #555;
        width: fit-content;
        padding: 16px;
        flex-direction: column;
        height: fit-content;
        gap: 0;
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
        gap: 16px;
        & p{
            &:not(:last-child):before{
                content: "/";
                cursor: auto;
                margin-right: 16px;
            }
            &:first-child{
                margin-right: 16px;
            }
            cursor: pointer;
        }
    }
</style>
