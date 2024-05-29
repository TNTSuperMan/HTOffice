<script setup>
import Item from "./item.vue"
const datas = defineModel()
const emit = defineEmits(["select"])
function select(idx){  
    emit("select",idx)
}
</script>
<template>
    <main>
        <Item v-for="(item,idx) in datas" :data="item" @click="select(idx)"/>
    </main>
</template>
<style scoped>
main{
    border:1px #000 solid;
}
</style>