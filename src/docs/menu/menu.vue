<script setup>
import { ref, watch } from "vue"
import Text from "./components/text.vue"
const m = defineModel()
const model = ref(m.value)
const item = ref(null)
watch(m,(nm)=>{
    model.value = nm;
    if(typeof model.value != "undefined" &&
    typeof model.value.type != "undefined" &&
    typeof model.value.data != "undefined"){
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
        <component v-if="typeof model !== 'undefined'"
        :is="item" v-model="model" @remove="$emit('remove')"/>
    </header>
</template>
<style scoped>
header{
    background:gray;
    height:100px;
}
</style>