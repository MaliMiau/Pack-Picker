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
        <div class="list">
            <ul v-for="category in Categories" :key="category as string">
                {{ category }}
                <li v-for="pack in Selected[category as keyof object]" :key="pack as string">
                    {{ pack }}
                </li>
            </ul>   
        </div>
        <button :disabled="JSON.stringify(Selected) === '{}'">Download</button>
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
    .title {
        background-color: black;
        color: white;
        font-size: x-large;
        height: 64px;
        line-height: 64px;
        text-align: center;
    }
    img {
        width: 320px;
        height: 180px;
        background-color: black;
        border: 0
    }
    ul {
        color: white;
        list-style-type: none;
        margin: 8px 24px 24px 16px;
        margin-top: 8px;
        padding: 0;
        font-size: x-large;
        &::before{
            content: "⬍ ";
            cursor: move;
        }
    }
    li {
        font-size: large;
        margin-left: 16px;
        &::before{
            content: "⬍ ";
            cursor: move;
        }
    }
    button {
        margin: -16px 16px 16px 16px;
        border: 0;
        background: #000000bb;
        border-radius: 16px;
        font-size: larger;
        line-height: 48px;
        transition: all 0.2s;
        &:hover{
            cursor: pointer;
            background: #888888bb;
        }
        &:disabled{
            background: #888888bb;
            color: silver;
        }
    }
    .list{
        max-height: 400px;
        margin: 0 16px 24px 8px;
        overflow-y: scroll;
        &::-webkit-scrollbar {
            width: 10px;
        }
        &::-webkit-scrollbar-track {
            background: none;
        }
        &::-webkit-scrollbar-thumb {
            background: #222;
            border-radius: 16px;
        }
        &::-webkit-scrollbar-thumb:hover {
            background: #555;
        }
    }
</style>
