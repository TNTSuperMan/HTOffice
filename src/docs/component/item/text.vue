<script setup>
import {ref} from "vue"
const props = defineProps(["data"])
const model = props.data
const data = ref({text:""});
if(typeof model != "undefined" &&
   typeof model.text != "undefined"){
    data.value = model;
}
</script>
<template>
    <pre>{{ data.text }}</pre>
</template>