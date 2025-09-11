<script setup>
import { ref, onMounted } from 'vue'
import Loader from './component/loader.vue'
import homePage from './pages/homePage.vue'

const isLoading = ref(true)

onMounted(() => {
  setTimeout(() => {
    isLoading.value = false
  }, 2000) // durasi loading, bisa diubah sesuai kebutuhan
})
</script>
  
<template>
  <Loader v-if="isLoading" />
  <homePage v-else />
</template>

<style scoped></style>
