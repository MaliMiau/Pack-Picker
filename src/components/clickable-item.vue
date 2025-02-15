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
        width: 150px;
        height: 175px;
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
        width: 80px;
        height: 80px;
        background-color: black;
        margin-top: 25px;
    }
    section {
        margin-top: 10px;
        color: white;
        font-family: 'Courier New', Courier, monospace;
        font-size: larger;
        text-align: center;
    }
</style>
