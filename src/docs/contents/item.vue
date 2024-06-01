<script setup>
import Text from "./components/text.vue"
const model = defineModel()
let item
switch(model.value.type){
    case "text":
        item = Text;
        break;
}
</script>
<template>
    <component :is="item" v-model="model.data"/>
</template>