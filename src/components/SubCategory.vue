<script setup lang="ts">
import { ref } from "vue";
import ClickableItems from './ClickableItems.vue';
const show = ref(false)

defineProps({
    SubCategory:{
        type: Object,
        default: JSON.parse('{"name": "Category", "packs": ["Pack"]}')
    },
    ParentName:{
        type: String,
        default: "Parent"
    }
})
</script>

<template>
    <div class="subcategory-container">
        <button @click="show = !show">{{ ParentName + " > " + SubCategory.name }}</button>
        <div class="grid" v-show="show">
            <ClickableItems v-for="pack in SubCategory.packs" :key="pack" :Name="pack"/>
        </div>
    </div>
</template>

<style scoped>
    .grid {
        display: grid;
        width: 170px;
        grid-template-columns: repeat(5, 1fr);
    }
    .subcategory-container {
        background-color: green;
        width: 814px;
        border-radius: 16px;
        overflow: hidden;
        margin-bottom: 16px;
    }
    button {
        width: 100%;
        height: 48px;
        background: #000000bb;
        border: 0;
        color: white;
        text-align: left;
        text-indent: 16px;
        font-size: large;
        &:hover {
            background: #000000ee;
            cursor: pointer;
        }
    }
</style>