<script setup>
import {ref} from "vue"
import Items from "./contents/contents.vue"
import Menu from "./menu/menu.vue"
const currentIdx = ref(-1)
const datas = ref([
    {
        type: "text",
        data:{
            text:"one",
            color:"#000000",
            background:undefined,
            size:30,
            weight:1000
        }
    },
    {
        type: "text",
        data:{
            text:"two",
            color:"#FF0000",
            background:undefined,
            size:30,
            weight:1000
        }
    },
    {
        type: "text",
        data:{
            text:"three",
            color:"#00FF00",
            background:undefined,
            size:30,
            weight:1000
        }
    },
    {
        type: "text",
        data:{
            text:"four",
            color:"#0000FF",
            background:undefined,
            size:30,
            weight:1000
        }
    },
])
function menu(idx){
    currentIdx.value = idx;
}
function remove(){
    let idx = currentIdx.value;
    //datas.value.splice(idx,1)
    //delete datas.value[idx]
    const datas_ = datas.value;
    let ret = datas_.filter(data => 
        data != datas_[idx]
    )
    console.log(ret)
    datas.value = ret;
    currentIdx.value = -1;
}
</script>
<template>
    <Menu v-model="datas[currentIdx]" @remove="remove"/>
    <Items v-model="datas" @select="menu"/>
</template>
