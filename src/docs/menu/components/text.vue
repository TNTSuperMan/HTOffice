<script setup>
import {ref} from "vue"
const model = defineModel()
function erase_back(){
    model.value.data.background = ""
}
</script>
<template>
    <textarea v-model="model.data.text"></textarea>
    <div class="next">
        <table>
            <tr>
                <th>文字色</th><td><input type="color" v-model="model.data.color"></td>
                <th>サイズ</th><td><input type="number" v-model="model.data.size" min="1" max="512"></td>
            </tr>
            <tr>
                <th>背景色</th><td><input type="color" v-model="model.data.background"></td>
                <th>太さ</th><td><input type="number" v-model="model.data.weight" step="100" min="0" max="1000"></td>
            </tr>
            <tr>
                <th>背景消去</th><td><button @click="erase_back">背景を消す</button></td>
                <th>文字消去</th><td><button @click="$emit('remove')">この文字を消す</button></td>
            </tr>
        </table>
    </div>

</template>
<style scoped>
textarea{
    height:90%;
    resize:horizontal;
}
div.next{
    float:right;
}
input[type=number]{
    width:60px;
}
</style>