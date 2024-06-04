<script setup>
const text = defineModel()
function update(e){
    text.value = e.target.innerText
}
</script>
<template>
    <td contenteditable="true" v-text="text" @input="update"></td>
</template>