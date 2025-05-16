<template>
  <div class="app-container">
    <h1 class="app-title">Как ты себя чувствуешь?</h1>
    <EmotionCircle />
  </div>
</template>

<script setup>
import EmotionCircle from './components/EmotionCircle.vue'
</script>

<style scoped>
.app-container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  height: 100vh;
  background-color: #faf9f6;
}

.app-title {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 30px;
  color: #333;
}
</style>
