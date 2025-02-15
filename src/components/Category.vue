<script setup lang="ts">
import Clickable from './Clickable.vue';
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
            <Clickable v-for="pack in packs":key="pack" :Name="pack"/>
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