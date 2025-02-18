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
    <div class="sidebar-container">
        <div class="title">Mali's Pack Picker</div>
        <img>
        <div>
            <ul v-for="category in Categories" :key="category as string">
                {{ category }}
                <li v-for="pack in Selected[category as keyof object]" :key="pack">
                    {{ pack }}
                </li>
            </ul>
        </div>
    </div>
</template>

<style scoped>
    .sidebar-container {
        width: 320px !important;
        height: fit-content;
        display: flex;
        flex-direction: column;
        gap: 16px;
        background-color: #000000bb;
    }
    .title{
        background-color: black;
        color: white;
        font-size: x-large;
        height: 64px;
        line-height: 64px;
        text-align: center;
    }
    img{
        width: 320px;
        height: 180px;
        background-color: black;
        border: 0
    }
    ul{
        color: white;
        list-style-type: none;
        margin: 24px;
        padding: 0;
        font-size: x-large;
        user-select: none;
        &::before{
            content: "⬍ ";
            cursor: move;
        }
    }
    li {
        font-size: large;
        margin-left: 16px;
        user-select: none;
        &::before{
            content: "⬍ ";
            cursor: move;
        }
    }
</style>
