<script setup>
import "./contents.css"
import Item from "./item.vue"
const datas = defineModel()
</script>
<template>
    <main>
        <Item v-for="(i,idx) in datas" v-model="datas[idx]" @click="$emit('menu',idx)"/>
    </main>
    <button @click="datas.push({type:'text',data:{text:'text',color:'#000',size:30,weight:100}})">+</button>
</template>
<style scoped>
main{
    border:1px #000 solid;
}
</style>