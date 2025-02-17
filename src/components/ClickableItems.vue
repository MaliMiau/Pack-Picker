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
        }
    })
    const active = ref("inactive")
    const toggle = () => {
        if (active.value === "inactive") active.value = "active"
        else active.value = "inactive"
    }
</script>

<template>
<div class="item-container" :class="active" @click="toggle();$emit('updateSelected', Name, active)">
    <img>
    <section>{{ Name }}</section>
    <div class="item-description">{{ Description }}</div>
</div>
</template>

<style scoped>
    * {
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    }
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
    }
    .item-container.active {
        background-color: #888888bb;
        &:hover{
            background: #aaaaaabb;
            cursor: pointer;
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
        font-weight: 600;
    }
    .item-description {
        color: white;
        position: absolute;
        width: inherit;
        text-align: center;
        padding: 10px 10px;
        border-radius: 16px;
        transform: translateY(-110%);
        background-color: #000000;
        display: none;
        filter: opacity(0);
        transition: all 10s;
    }
    .item-container:hover .item-description {
        display: block;
        filter: opacity(1);
    }
</style>
