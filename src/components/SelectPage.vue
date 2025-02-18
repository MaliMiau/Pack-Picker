<script setup lang="ts">
    import { ref } from 'vue';
    import AllCategories from './AllCategories.vue';
    import SideBar from './SideBar.vue';
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
        console.log(selected.value)
    }
    
</script>

<template>
    <div>
        <AllCategories :json="json" @update-selected="(n, a, c) => updateSelected(n, a, c)"/>
        <SideBar :Categories="Object.keys(selected)" :Selected="selected"/>
    </div>
</template>

<style scoped>
    div{
        display: flex;
        flex-direction: row;
        width: 100%;
        justify-content: center;
        gap: 20px;
    }
</style>
