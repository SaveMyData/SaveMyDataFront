<script setup lang="ts">
import { useRouter } from 'vue-router'

const router = useRouter()

const handleNavigate = (destination: string) => {
  if (destination === 'register') {
    router.push({ name: 'Register' })
  }
  if (destination === 'dashboard') {
    router.push({ name: 'Dashboard' })
  }
  if (destination === 'login') {
    router.push({ name: 'Login' })
  }
}
</script>


<template>
  <router-view @navigate="handleNavigate"/>
</template>
