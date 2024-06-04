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
    datas.value.splice(currentIdx.value, 1)
    currentIdx.value = -1;
}
const isCanSSFP = typeof window.showSaveFilePicker != "undefined"
const url = ref("")
const dlr = ref()
function save(){
    if(typeof window.showSaveFilePicker != "undefined"){
        window.showSaveFilePicker({
            suggestedName: "document",
            types:[{
                description: "HTOffice Docs",
                accept: {"application/json": [".htod"]}
            }]
        }).then(e=>e.createWritable()).then(f=>{
            f.write(JSON.stringify(datas.value))
                .then(e=>f.close())
        })
    }else{
        let blob = URL.createObjectURL(new Blob([
            JSON.stringify(datas.value)],{
            type: "application/json"}))
        url.value = blob
        dlr.value.click()
        setTimeout(e=>URL.revokeObjectURL(blob),20000)
    }
}
const upr = ref()
function load(e){
    const reader = new FileReader()
    reader.addEventListener("load",t=>{
        try{
            datas.value = JSON.parse(t.target.result)
        }
        catch{
            alert("有効なHTOffice Docsファイルではありません")
        }
    })
    reader.readAsText(e.target.files[0])
}
</script>
<template>
    <a v-if="isCanSSFP" ref="dlr" :href="url" download="document.hod"></a>
    <input ref="upr" v-show="false" type="file"
    accept=".htod, application/json" @change="load">
    <Menu v-model="datas[currentIdx]" @remove="remove" 
    @save="save" @load="upr.click()"/>
    <Items v-model="datas" @menu="menu"/>
</template>