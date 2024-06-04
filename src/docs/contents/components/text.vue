<script setup>
import {computed, ref} from "vue"
const model = defineModel()
const text = ref(model.value.text)
const style = computed(e=>{
    let s = "";
    let m = model.value;
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
    return s
})
function updateText(e){
    model.value.text = e.target.innerText
}
</script>
<template>
    <span contenteditable="true" v-text="text" :style="style" @input="updateText"></span>
</template>
<style scoped>
span{
    word-break:break-all;
    overflow-wrap:anywhere;
}
span:focus-visible{
    outline:none;
}
</style>