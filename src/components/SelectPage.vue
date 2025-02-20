<script setup lang="ts">
    import { ref } from 'vue';
    import AllCategories from './AllCategories.vue';
    import SideBar from './SideBar.vue';
    import json from '../assets/test-json/properties.json'
    const selected = ref({})
    const selectedVersion = ref(0 as number)
    const possibleIncompatibilities = ref([] as string[])
    const knownIncompatibilities = ref([] as string[])

    const updateSelected = (name:string, active:string, category: string) => {
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
        if(json.versions[selectedVersion.value].incompatibilities?.[pack as keyof object] === undefined) return
        
        if(add){
            possibleIncompatibilities.value.push(pack)

            if(possibleIncompatibilities.value.length > 1){
                possibleIncompatibilities.value.every((name: string) => {
                    let incompatibilites_temp = json.versions[selectedVersion.value].incompatibilities?.[name as keyof object] as unknown as string[]
                    if(incompatibilites_temp.indexOf(pack) === -1) return true

                    knownIncompatibilities.value.push(pack)
                    return false
                })
            }
        }
        else{
            let index = possibleIncompatibilities.value.indexOf(pack)
            possibleIncompatibilities.value.splice(index, 1)
            index = knownIncompatibilities.value.indexOf(pack)
            knownIncompatibilities.value.splice(index, 1)
            updateIncompatibilities()
        }
    }
    const updateIncompatibilities = () => {
        knownIncompatibilities.value = []
        possibleIncompatibilities.value.every((curr: string, curr_index: number) => {
            if(curr_index === 0) return true

            possibleIncompatibilities.value.every((prev: string, prev_index: number) => {
            if(prev_index >= curr_index) return false
            let incompatibilites_temp = json.versions[selectedVersion.value].incompatibilities?.[prev as keyof object] as unknown as string[]
            if(incompatibilites_temp.indexOf(curr) === -1) return true
            knownIncompatibilities.value.push(curr)
            return false
            })

        })
    }

    const sortedItems = (category: string, arrayItems: Array<string>) => {
        console.log(arrayItems, category)
        console.log(selected.value)
        selected.value[category as keyof object] = arrayItems as never
        console.log(selected.value)
    }
    const sortedCategories = (arrayCategories: Array<string>) => {
        console.log(arrayCategories)
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
