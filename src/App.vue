<script setup>
import { ref, onMounted } from 'vue';

const telegramInitialized = ref(false);
const user = ref(null);

onMounted(() => {
  if (window.Telegram?.WebApp) {
    window.Telegram.WebApp.ready();
    telegramInitialized.value = true;

    const initData = window.Telegram.WebApp.initDataUnsafe;
    console.log("initDataUnsafe:", initData);

    if (initData?.user) {
      user.value = initData.user;
    } else {
      console.warn("User data not found in initDataUnsafe");
    }
  } else {
    console.warn("Telegram WebApp not found");
  }
});
</script>

<template>
  <div class="container">
    <h1>Добро пожаловать в Mini App</h1>

    <p v-if="!telegramInitialized">❌ Telegram WebApp не инициализирован</p>
    <p v-else-if="user">✅ Инициализирован как {{ user.first_name }} (ID: {{ user.id }})</p>
    <p v-else>⚠️ Telegram SDK есть, но пользователь не передан</p>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  font-family: sans-serif;
}
</style>
