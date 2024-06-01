<script setup>
import { computed } from "vue"
import "../../assets/docs.css"
import Item from "./item.vue"
const datas = defineModel()
</script>
<template>
    <main>
        <Item v-for="(i,idx) in datas" v-model="datas[idx]" @click="$emit('menu',idx)"/>
    </main>
    <button @click="datas.push({type:'text',data:{text:'text'}})">+</button>
</template>
<style scoped>
main{
    border:1px #000 solid;
}
</style>