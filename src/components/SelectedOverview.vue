<script setup lang="ts">
    defineProps({
        Categories: {
            type:Array,
            required: true
        },
        Selected: {
            type:Object,
            required: true
        }
    })
</script>

<template>
    <div>selected:
        <ul v-for="category in Categories" :key="category as string">
            {{ category }}
            <li v-for="pack in Selected[category as keyof object]" :key="pack">
                {{ pack }}
            </li>
        </ul>
    </div>
</template>

<style scoped>

</style>
