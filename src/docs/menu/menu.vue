<script setup>
import { ref, watch } from "vue"
import Button from "./components/button.vue"
import Text from "./components/text.vue"
const model = defineModel()
const item = ref(null)
watch(model,m=>{
    if(typeof m != "undefined" &&
    typeof m.type != "undefined" &&
    typeof m.data != "undefined"){
        switch(m.type){
            case "text":
                item.value = Text;
                break;
        }
    }
})

</script>
<template>
    <header>
        <details>
            <summary>ファイル</summary>
            <Button text="保存" @click="$emit('save')" />
            <Button text="読込" @click="console.log('UP')" />
            <Button text="HTMLとしてエクスポート" @click="console.log('EX')" />
        </details>
        
        <component v-if="typeof model !== 'undefined'"
        :is="item" v-model="model" @remove="$emit('remove')"/>
    </header>
</template>
<style scoped>
header{
    background:gray;
}
details{
    cursor:pointer;
    display:inline;
    font-size:20px;
    background:white;
    border-radius: 5px;
    border:1px black solid;
    padding:5px;
    margin:2px;
}
</style>