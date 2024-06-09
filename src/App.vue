<script setup>
import { ref, computed } from 'vue'
import Home from "./home/home.vue"
import Credit from "./credit/credit.vue"
import Docs from "./docs/docs.vue"
import Table from "./table/table.vue"

const path = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  path.value = window.location.hash
})

const currentPage = computed(() => {
  return {
    '/': Home,
    'credit': Credit,
    'docs': Docs,
    'table': Table
  }[path.value.slice(1) || '/'] || Home
})
</script>
<template>
  <component :is="currentPage" />
</template>
<style>
body{
  background:#333;
}
</style>