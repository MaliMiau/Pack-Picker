<script setup lang="ts">
    import { ref } from 'vue';
    import AllCategories from './AllCategories.vue';
    import SelectedOverview from './SelectedOverview.vue';
    import json from '../test-json/properties.json'
    const selected = ref({})

    const updateSelected = (name:string, active:string, category: string) => {
        console.log(name, active, category)
        if(selected.value[category as keyof object] === undefined){
            selected.value[category as keyof object] = []
        }
        if(active === "active") selected.value[category as keyof object].push(name)
        if(active === "inactive") {
            let index = selected.value[category as keyof object].indexOf(name)
            selected.value[category as keyof object].splice(index, 1)
            if(selected.value[category as keyof object].length === 0){
                delete selected.value[category as keyof object]
            }
        }
    }
    
</script>

<template>
    <AllCategories :json="json" @update-selected="(n, a, c) => updateSelected(n, a, c)"/>
    <SelectedOverview :Categories="Object.keys(selected)" :Selected="selected"/>
</template>

<style scoped>

</style>
