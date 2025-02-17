<script setup lang="ts">
    import { ref } from 'vue';
    import AllCategories from './AllCategories.vue';
    import SelectedOverview from './SelectedOverview.vue';
    import json from '../test-json/properties.json'
    const selected = ref({})

    const updateSelected = (name:string, active:string, category: string) => {
        console.log(name, active, category)
        let selected_temp = selected.value[category as keyof object] as string[]
        if(selected_temp === undefined){
            selected_temp = []
        }
        if(active === "active") selected_temp.push(name)
        if(active === "inactive") {
            let index = selected_temp.indexOf(name)
            selected_temp.splice(index, 1)
            if(selected_temp.length === 0){
                delete selected.value[category as keyof object]
                return
            }
        }
        selected.value[category as keyof object] = selected_temp as never
    }
    
</script>

<template>
    <AllCategories :json="json" @update-selected="(n, a, c) => updateSelected(n, a, c)"/>
    <SelectedOverview :Categories="Object.keys(selected)" :Selected="selected"/>
</template>

<style scoped>

</style>
