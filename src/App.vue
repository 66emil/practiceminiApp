<script setup>
import { ref, onMounted } from 'vue';

const telegramInitialized = ref(false);

onMounted(() => {
  if (window.Telegram && window.Telegram.WebApp) {
    telegramInitialized.value = true;
    window.Telegram.WebApp.ready();
  } else {
    telegramInitialized.value = false;
  }
});
</script>

<template>
  <div>
    <h1>Добро пожаловать в Mini App</h1>
    <p v-if="!telegramInitialized">Telegram WebApp не инициализирован</p>
    <p v-else>Telegram WebApp успешно инициализирован!</p>
  </div>
</template>

<style scoped>
.container {
  padding: 20px;
  font-family: sans-serif;
}
</style>
