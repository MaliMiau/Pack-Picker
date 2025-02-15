<script setup lang="ts">
import { ref } from "vue";
import ClickableItems from './ClickableItems.vue';
import SubCategory from './SubCategory.vue';
const show = ref(true)

defineProps({
    Category:{
        type: Object,
        default: JSON.parse('{"name": "Category", "packs": ["Pack"]}')
    }
})
</script>

<template>
    <div class="category-container">
        <button @click="show = !show">{{ Category.name }}</button>
        <div class="content" v-show="show">
            <div class="grid">
                <ClickableItems v-for="pack in Category.packs" :key="pack" :Name="pack"/>
            </div>
            <SubCategory v-for="subcategory in Category.subcategories" :key="subcategory.name" :SubCategory="subcategory" />
        </div>
    </div>
</template>

<style scoped>
    .grid {
        display: grid;
        width: fit-content;
        grid-template-columns: repeat(6, 1fr);
    }
    .category-container {
        background-color: red;
        width: 962px;
        margin-top: 16px;
        border-radius: 16px;
        overflow: hidden;
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
    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
    }
</style>