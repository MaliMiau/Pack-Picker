<script setup lang="ts">
    import { ref } from "vue";
    import ClickableItems from './ClickableItems.vue';
    const show = ref(false)

    defineProps({
        SubCategory:{
            type: Object,
            default: () => ({"name": "Category", "packs": [{"name":"Pack", "description":"Description"}]})
        },
        ParentName:{
            type: String,
            default: "Parent"
        },
        Incompatibilities:{
            type: Array,
            default: () => [""]
        },
        jsonIncompatibilities:{
            type: Object,
            required: true
        }
    })
</script>

<template>
    <div class="subcategory-container">
        <button @click="show = !show">
            {{ ParentName }}
            >
            <b> {{ SubCategory.name }} </b>
        </button>
        <div class="grid" :class="show ? 'show' : 'hide'">
            <ClickableItems 
                v-for="pack in SubCategory.packs" 
                :key="pack" 
                :Name="pack" 
                :Incompatibilities="Incompatibilities"
                :SelfIncompatibilities="jsonIncompatibilities[pack]"
                @update-selected="(n, a) => $emit('updateSelected', n, a)"
            />
        </div>
    </div>
</template>

<style scoped>
    .grid {
        display: grid;
        width: 170px;
        grid-template-columns: repeat(5, 1fr);
        transition: height 0.5s;
        interpolate-size: allow-keywords;
    }
    .subcategory-container {
        background: #00000066;
        width: 814px;
        margin-bottom: 16px;
        border-radius: 16px;
        overflow: hidden;
        box-shadow: inset 0 0 0 8px #00000066;
    }
    button {
        width: 100%;
        height: 48px;
        background: #000000bb;
        border: 0;
        color: silver;
        text-align: left;
        text-indent: 16px;
        font-size: large;
        font-weight: 400;
        &:hover {
            background: #000000ee;
            cursor: pointer;
        }
    }

    .grid.hide{
        height: 0;
    }
</style>