<script setup>
import {ref} from "vue"
import Items from "./component/items.vue"
import Menu from "./component/menu.vue"
const currentIdx = ref(-1)
const datas = ref([
    {
        type: "text",
        data:{
            text:"Hello,World!\nGood Document!"
        }
    }
])
function menu(idx){
    currentIdx.value = idx;
}
</script>
<template>
    <Menu v-model="datas[currentIdx]" />
    <Items v-model="datas" @select="menu"/>
</template>