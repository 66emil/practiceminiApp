<template>
  <div class="container">
    <h1>Добро пожаловать в Mini App</h1>

    <div v-if="user">
      <p>Пользователь: {{ user.first_name }} (ID: {{ user.id }})</p>
    </div>
    <div v-else>
      <p>Telegram WebApp не инициализирован</p>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from 'vue'

const user = ref(null)

onMounted(() => {
  console.log("App mounted")

  if (window.Telegram?.WebApp) {
    window.Telegram.WebApp.ready()
    console.log("Telegram SDK detected")

    const tgUser = window.Telegram.WebApp.initDataUnsafe?.user
    console.log("User:", tgUser)

    if (tgUser) {
      user.value = tgUser
    }
  } else {
    console.log("Telegram.WebApp not found")
  }
})
</script>

<style scoped>
.container {
  padding: 20px;
  font-family: sans-serif;
}
</style>
