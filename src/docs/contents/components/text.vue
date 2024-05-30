<script setup>
import {ref, watch} from "vue"
const model = defineModel()
const text = ref(model.value.text)
const style = ref("")
function updateModel(m){
    text.value = m.text;
    style.value = ""
    if(typeof m.background == "string"){
        style.value += "background:" + m.background + ";";
    }
    if(typeof m.color == "string"){
        style.value += "color:" + m.color + ";";
    }
    if(typeof m.size == "number"){
        style.value += "font-size:" + m.size + "px;";
    }
    if(typeof m.weight == "number"){
        style.value += "font-weight:" + m.weight + ";";
    }
}
updateModel(model.value)
watch(model.value,updateModel)
function updateText(e){
    model.value.text = e.target.innerText
}
</script>
<template>
    <span contenteditable="true" v-text="text" :style="style" @input="updateText"></span>
</template>