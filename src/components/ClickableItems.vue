<script setup lang="ts">
defineProps({
    Name:{
        type: String,
        default: "Pack"
    }
})
</script>

<template>
<div>
    <img>
    <section>{{ Name }}</section>
</div>
</template>

<style scoped>
    div{
        background: #000000aa;
        width: 128px;
        height: 160px;
        margin: 10px;
        border-radius: 24px;
        display: flex;
        flex-direction: column;
        align-items: center;
        &:hover{
            background: #000000ee;
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
        font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
        font-size: larger;
        text-align: center;
        margin: 10px 5px;
        font-weight: 600;
    }
</style>
