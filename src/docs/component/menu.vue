<script setup>
import { ref, watch } from "vue"
import Text from "./menu/text.vue"
const m = defineModel()
const model = ref(m.value)
const item = ref(null)
watch(m,(nm)=>{
    model.value = nm;
    if(typeof model.value != "undefined" &&
    typeof model.value.type != "undefined" &&
    typeof model.value.data != "undefined"){
        console.log(model.value)
        switch(model.value.type){
            case "text":
                item.value = Text;
                break;
        }
}
})

</script>
<template>
    <header>
        <component :is="item" v-model="model"/>
    </header>
</template>
<style scoped>
header{
    background:gray;
    height:75px;
}
</style>