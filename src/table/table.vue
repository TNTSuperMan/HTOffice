<script setup>
import {reactive, ref, watch} from "vue"
import Item from "./components/item.vue"
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
    console.log(m)
}
watch(data,updTable)
updTable()
</script>
<template>
    <table border>
        <tr><th></th><th v-for="m in max">{{ m }}</th></tr>
        <tr v-for="(dat,i) in data">
            <th>{{ i + 1 }}</th>
            <Item v-for="(d,j) in dat" v-model="data[i][j]"/>
        </tr>
    </table>
</template>
<style scoped>
th,td{
    padding:5px
}
</style>