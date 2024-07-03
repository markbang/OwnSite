<script setup lang="ts">
import { RouterLink, RouterView } from 'vue-router'
import AutoCome from './components/AutoCom.vue'
</script>

<template>
  <h1 class="text-3xl font-bold underline bg-red-500 text-red-400">
    Hello world!
  </h1>
  <AutoCome />
  <RouterView />
</template>

<style scoped>

</style>
