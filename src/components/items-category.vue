<script setup lang="ts">
import clickableItem from './clickable-item.vue';
const packs = [
    "1",
    "2",
    "Rose Quartzzzzz",
    "4",
    "1",
    "2",
    "Rose Quartzzzzz",
    "4",
    "1",
    "2",
    "Rose Quartzzzzz",
    "4",
]
</script>

<template>
    <div class="container">
        <div class="grid">
            <clickableItem v-for="pack in packs" :key="pack" :Name="pack"/>
        </div>
    </div>
    
</template>

<style scoped>
.grid {
    display: grid;
    width: 170px;
    grid-template-columns: repeat(6, 1fr);
}
</style>