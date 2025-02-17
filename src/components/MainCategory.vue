<script setup lang="ts">
    import { ref } from "vue";
    import ClickableItems from './ClickableItems.vue';
    import SubCategory from './SubCategory.vue';
    const show = ref("hide")

    const props = defineProps({
        Category:{
            type: Object,
            default: JSON.parse('{"name": "Category", "packs": ["Pack"]}')
        },
        Index:{
            type: Number,
            default: 1
        }
    })
    if(props.Index === 0) show.value = "show"
    const toggle = () => {
        if (show.value == "hide") show.value = "show"
        else show.value = "hide"
        console.log(show.value)
    }
</script>

<template>
    <div class="category-container">
        <button @click="toggle">{{ Category.name }}</button>
        <div class="content" :class="show">
            <div class="grid">
                <ClickableItems v-for="pack in Category.packs" :key="pack" :Name="pack.name" :Description="pack.description" @update-selected="(n, a) => $emit('updateSelected', n, a, Category.name)"/>
            </div>
            <SubCategory v-for="subcategory in Category.subcategories" :key="subcategory.name" :SubCategory="subcategory" @update-selected="(n, a) => $emit('updateSelected', n, a, Category.name)"/>
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
        background: #00000066;
        width: 962px;
        margin-top: 16px;
        border-radius: 16px;
        overflow: hidden;
        box-shadow: inset 0 0 0 8px #00000066;
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
        cursor: pointer;
    }
    .content {
        display: flex;
        flex-direction: column;
        align-items: center;
        transition: height 0.5s;
        interpolate-size: allow-keywords;
    }
    .content.hide{
        height: 0;
    }
</style>