<script setup>
import {ref} from "vue"
import Items from "./contents/contents.vue"
import Menu from "./menu/menu.vue"
const currentIdx = ref(-1)
const datas = ref([])
const menu=idx=>{currentIdx.value = idx;}
function remove(){
    datas.value.splice(currentIdx.value, 1)
    currentIdx.value = -1;
}
const isCanSSFP = typeof window.showSaveFilePicker != "undefined"
const url = ref("")
const dlr = ref()
function save(){
    let fobj = []
    datas.value.forEach(e=>
        fobj.push({type:e.type,data:e.data})
    )
    let fdat = JSON.stringify(datas.value)
    if(isCanSSFP){
        window.showSaveFilePicker({
            suggestedName: "document",
            types:[{
                description: "HTOffice Docs",
                accept: {"application/json": [".htod"]}
            }]
        }).then(e=>e.createWritable()).then(f=>
            f.write(fdat).then(e=>f.close())
        )
    }else{
        let blob = URL.createObjectURL(
            new Blob([fdat],{
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
function exashtml(){
    let data = "<!doctype html>"
    data += "<!-- Powered by HTOffice Docs. -->"
    data += "<!-- https://github.com/TNTSuperMan/HTOffice -->"
    data += "<html lang='ja'>"
    data += "<head>"
    data += "<style>"
    data += "*{font-family:sans-serif;}"
    data += "span{white-space:pre;}"
    data += "</style>"
    data += "<meta charset='UTF-8'>"
    data += "<meta name='viewport' content='width=device-width, initial-scale=1.0'>"
    data += "</head><body>"
    datas.value.forEach(e=>{
        data += e.dom
    })
    data += "</body></html>"
    if(isCanSSFP){
        window.showSaveFilePicker({
            suggestedName: "document",
            types:[{
                description: "HTML Document",
                accept: {"text/html": [".html"]}
            }]
        }).then(e=>e.createWritable()).then(f=>{
            f.write(data)
                .then(e=>f.close())
        })
    }else{

    }
}
</script>
<template>
    <a v-if="isCanSSFP" ref="dlr" :href="url" download="document.hod"></a>
    <input ref="upr" v-show="false" type="file"
    accept=".htod, application/json" @change="load">
    <Menu v-model="datas[currentIdx]" @remove="remove" 
    @save="save" @load="upr.click()" @exp="exashtml"/>
    <Items v-model="datas" @menu="menu"/>
</template>