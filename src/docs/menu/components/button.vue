<script setup>
const props = defineProps(["text"])
</script>
<template>
    <button>{{ props.text }}</button>
</template>
<style scoped>
button{
    background:#eee;
    /*font-size:20px;*/
    border-radius: 5px;
    cursor:pointer;
}
</style>