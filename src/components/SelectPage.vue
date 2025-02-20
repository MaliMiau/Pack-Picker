<script setup lang="ts">
    import { ref } from 'vue';
    import AllCategories from './AllCategories.vue';
    import SideBar from './SideBar.vue';
    import json from '../assets/test-json/properties.json'
    const selected = ref({})
    const selectedVersion = ref(0)
    const possibleIncompatibilities = ref([] as string[])
    const knownIncompatibilities = ref([] as string[])

    const updateSelected = (name:string, active: boolean, category: string) => {
        let selected_temp = selected.value[category as keyof object] as string[]
        if(selected_temp === undefined){
            selected_temp = []
        }
        if(active) {
            selected_temp.push(name)
            checkIncompatibilities(name, true)
        }
        else {
            let index = selected_temp.indexOf(name)
            selected_temp.splice(index, 1)
            checkIncompatibilities(name, false)
            if(selected_temp.length === 0){
                delete selected.value[category as keyof object]
                return
            }
        }
        selected.value[category as keyof object] = selected_temp as never
    }

    const checkIncompatibilities = (pack: string, add: boolean) => {
        let incom_obj = json.versions[selectedVersion.value].incompatibilities as object
        if(incom_obj[pack as keyof object] === undefined) return
        
        if(add){
            possibleIncompatibilities.value.push(pack)
            updateKnownIncompatibilities()
        }
        else{
            let index = possibleIncompatibilities.value.indexOf(pack)
            possibleIncompatibilities.value.splice(index, 1)
            updateKnownIncompatibilities()
        }
    }
    const updateKnownIncompatibilities = () => {
        knownIncompatibilities.value = []
        let poss_incom = possibleIncompatibilities.value
        let incompatibilities_temp
        poss_incom.every((curr: string, curr_index: number) => {
            if(curr_index === 0) return true

            poss_incom.every((prev: string, prev_index: number) => {
                if(prev_index >= curr_index) return false

                incompatibilities_temp = json.versions[selectedVersion.value].incompatibilities?.[prev as keyof object] as unknown as string[]
                if(!incompatibilities_temp.includes(curr)) return true
                knownIncompatibilities.value.push(curr)
                return false
            })
            return true
        })
    }

    const sortedItems = (category: string, arrayItems: Array<string>) => {
        selected.value[category as keyof object] = arrayItems as never
        updatePossibleIncompatibilities()
    }
    const sortedCategories = (arrayCategories: Array<string>) => {
        let new_selected: object = {}
        arrayCategories.every((category: string) => {
            new_selected[category as keyof object] = selected.value[category as keyof object] as never
            return true
        })
        selected.value = new_selected
        updatePossibleIncompatibilities()
    }
    const updatePossibleIncompatibilities = () => {
        let categories = Object.keys(selected.value)
        let selectedCategory
        let incom_obj
        possibleIncompatibilities.value = []
        categories.forEach((category) => {
            selectedCategory = selected.value[category as keyof object] as string[]
            selectedCategory.forEach(pack => {
                incom_obj = json.versions[selectedVersion.value].incompatibilities as object
                if(incom_obj[pack as keyof object] === undefined) return
                possibleIncompatibilities.value.push(pack)
            });
        })
        updateKnownIncompatibilities()
    }
</script>

<template>
    <div>
        <AllCategories 
            :json="json" 
            :Incompatibilities="knownIncompatibilities"
            :jsonIncompatibilities="json.versions[selectedVersion].incompatibilities as unknown as object"
            @update-selected="(n, a, c) => updateSelected(n, a, c)" 
            @update-version="(v) => selectedVersion = v"
        />

        <SideBar 
            :Categories="Object.keys(selected)" 
            :Selected="selected"
            :Incompatibilities="knownIncompatibilities"
            @sorted-items="(c, a) => sortedItems(c, a)"
            @sorted-categories="(a) => sortedCategories(a)"
        />
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
