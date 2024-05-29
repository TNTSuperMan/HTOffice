<script setup>
import { ref, computed } from 'vue'
import Home from "./home/home.vue"
import Docs from "./docs/docs.vue"

const path = ref(window.location.hash)

window.addEventListener('hashchange', () => {
  path.value = window.location.hash
})

const currentPage = computed(() => {
  return {
    '/': Home,
    'docs': Docs
  }[path.value.slice(1) || '/'] || Home
})
</script>
<template>
  <component :is="currentPage" />
</template>
