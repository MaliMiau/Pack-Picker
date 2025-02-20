<script setup lang="ts">
    import { ref } from 'vue';
    defineProps({
        Name:{
            type: String,
            default: "Pack"
        },
        Description:{
            type: String,
            default: "Description"
        },
        Incompatibilities:{
            type: Array,
            required: true
        },
        SelfIncompatibilities:{
            type: Array,
            default: () => [""]
        }
    })
    const active = ref(false)
</script>

<template>
    <div 
    class="item-container" 
    :class="[
        active ? 'active': 'inactive', 
        Incompatibilities.includes(Name) ? 'incompatible' : 'compatible'
    ]" 
    @click="active = !active;$emit('updateSelected', Name, active)">
        <img>
        <section>{{ Name }}</section>
        <div class="item-widget item-description" v-html="Description"></div>
        <div class="item-widget item-incompatibilities">
            Incompatible with: 
            <i v-for="(name, index) in SelfIncompatibilities" :key="name as string">
                {{ name }}{{ index < SelfIncompatibilities.length-1 ? ", " : "." }}
            </i>
        </div>
    </div>
</template>

<style scoped>
    .item-container {
        background: #000000bb;
        width: 128px;
        height: 160px;
        border-radius: 24px;
        margin: 16px;
        display: flex;
        flex-direction: column;
        align-items: center;
        transition: all 0.2s;
        &:hover{
            background: #444444bb;
            cursor: pointer;
        }
        &.incompatible{
            background: #cc0000bb !important;
        }
        &.active {
            background-color: #888888bb;
            &:hover{
                background: #aaaaaabb;
                cursor: pointer;
            }
        }
    }
    img {
        width: 64px;
        height: 64px;
        background-color: black;
        margin-top: 25px;
    }
    section {
        color: white;
        font-size: larger;
        text-align: center;
        margin: 10px 5px;
    }
    .item-widget {
        color: white;
        position: absolute;
        text-align: center;
        padding: 10px 10px;
        border-radius: 16px;
        display: none;
        filter: opacity(0);
        transition: all 10s;
    }
    .item-description {
        width: inherit;
        font-weight: 300;
        transform: translateY(-110%);
        background-color: #000000;
    }
    .item-incompatibilities {
        width: fit-content;
        transform: translateY(168px);
        background-color: #cc0000;
    }
    .item-container:hover .item-description:not(:hover),
    .item-container.incompatible:hover .item-incompatibilities:not(:hover) {
        display: block;
        filter: opacity(1);
    }
</style>
