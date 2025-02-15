<script setup lang="ts">
import { ref } from "vue";
import ClickableItems from './ClickableItems.vue';
const show = ref(false)

defineProps({
    SubCategory:{
        type: Object,
        default: JSON.parse('{"name": "Category", "packs": ["Pack"]}')
    }
})
</script>

<template>
    <div class="container">
        <button @click="show = !show">Toggle</button>
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
</style>