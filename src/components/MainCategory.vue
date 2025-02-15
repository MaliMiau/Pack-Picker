<script setup lang="ts">
import ClickableItems from './ClickableItems.vue';
import SubCategory from './SubCategory.vue';
defineProps({
    Category:{
        type: Object,
        default: JSON.parse('{"name": "Category", "packs": ["Pack"]}')
    }
})
</script>

<template>
    <div class="category-container">
        <div class="grid">
            <ClickableItems v-for="pack in Category.packs" :key="pack" :Name="pack"/>
        </div>
        <SubCategory v-for="subcategory in Category.subcategories" :key="subcategory.name" :SubCategory="subcategory"/>
    </div>
</template>

<style scoped>
.grid {
    display: grid;
    width: 170px;
    grid-template-columns: repeat(6, 1fr);
}
</style>