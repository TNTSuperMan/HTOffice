<script setup>
import { ref, watch } from "vue"
import Text from "./components/text.vue"
const model = defineModel()
const item = ref(null)
watch(model,m=>{
    console.log(m)
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