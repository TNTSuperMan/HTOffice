<script setup>
import {reactive, ref, watch} from "vue"
import Item from "./components/item.vue"
import Home from "../hbtn.vue"
const data = reactive([
    [
        "aaa",
        "bbb",
        "ccc"
    ],[
        "ddd",
        "eee",
        "fff"
    ]
])
const max = ref([])
function updTable(){
    let m = 0
    data.forEach(t=>{
        if(m < t.length) m = t.length
    })
    max.value = [];
    for(let i = 0;i < m;i++){
        max.value.push(i + 1)
    }
}
watch(data,updTable)
updTable()
</script>
<template>
    <Home color="#000"/>
    <table border>
        <tr><th></th><th v-for="m in max">{{ m }}</th>
            <th><button @click="data.forEach(e=>e.push(''))">+</button></th>
            <th><button @click="data.forEach(e=>e.pop())">-</button></th>
        </tr>
        <tr v-for="(dat,i) in data">
            <th>{{ i + 1 }}</th>
            <Item v-for="(d,j) in dat" v-model="data[i][j]"/>
        </tr>
        <tr><button @click="data.push([])&&max.forEach(e=>data[data.length-1].push(''))">+</button></tr>
        <tr><button @click="data.pop()">-</button></tr>
    </table>
</template>
<style scoped>
th,td{
    padding:5px
}
</style>