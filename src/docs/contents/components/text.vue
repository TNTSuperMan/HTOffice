<script setup>
import {computed, ref} from "vue"
const model = defineModel()
const text = ref(model.value.data.text)
const style = computed(e=>{
    let s = "";
    let m = model.value.data;
    text.value = m.text;
    style.value = ""
    if(typeof m.background == "string"){
        s += "background:" + m.background + ";";
    }
    if(typeof m.color == "string"){
        s += "color:" + m.color + ";";
    }
    if(typeof m.size == "number"){
        s += "font-size:" + m.size + "px;";
    }
    if(typeof m.weight == "number"){
        s += "font-weight:" + m.weight + ";";
    }
    let data = "<span style='";
    data += s;
    data += "'>";
    data += text.value;
    data += "</span>";
    model.value.dom = data;
    return s
})
function updateText(e){
    model.value.data.text = e.target.innerText
}
</script>
<template>
    <span contenteditable="true" v-text="text" :style="style" @input="updateText"></span>
</template>
<style scoped>
span:focus-visible{
    outline:none;
}
</style>