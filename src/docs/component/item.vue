<script setup>
import Text from "./item/text.vue"
const props = defineProps(["data"])
const model = props.data
let item, data
if(typeof model != "undefined" &&
   typeof model.type != "undefined" &&
   typeof model.data != "undefined"){
    data = model.data
    switch(model.type){
        case "text":
            item = Text;
            break;
    }
}else{
}
</script>
<template>
    <component :is="item" :data="data"/>
</template>