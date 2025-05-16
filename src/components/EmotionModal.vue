<template>
  <div class="modal-overlay" @click="close">
    <div class="modal-content" :style="{ borderColor: emotion.color }" @click.stop>
      <header class="modal-header" :style="{ backgroundColor: emotion.color }">
        <h2 class="modal-title">{{ emotion.emoji }} {{ emotion.name }}</h2>
      </header>

      <div class="modal-body">
        <section>
          <h3>Описание</h3>
          <p>{{ emotion.description }}</p>
        </section>

        <section>
          <h3>Как ощущается в теле</h3>
          <p>{{ emotion.body }}</p>
        </section>

        <section>
          <h3>Что делать</h3>
          <p>{{ emotion.recommendations }}</p>
        </section>

        <section>
          <h3>Чего избегать</h3>
          <p>{{ emotion.avoid }}</p>
        </section>
      </div>

      <footer class="modal-footer">
        <button class="close-button" @click="close">Закрыть</button>
      </footer>
    </div>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
  emotion: Object,
})

const emit = defineEmits(['close'])

const close = () => {
  emit('close')
}
</script>

<style scoped>
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  animation: fadeIn 0.3s ease;
}

.modal-content {
  background-color: #ffffff;
  width: 350px;
  max-width: 90%;
  padding: 20px;
  border-radius: 16px;
  border: 4px solid;
  box-shadow: 0px 10px 20px rgba(0, 0, 0, 0.1);
  overflow: hidden;
  animation: slideUp 0.4s ease;
  display: flex;
  flex-direction: column;
}

.modal-header {
  padding: 10px;
  border-radius: 12px 12px 0 0;
  color: #ffffff;
  font-family: 'Poppins', sans-serif;
  font-weight: 700;
  text-align: center;
}

.modal-body {
  padding: 15px;
}

.modal-body section {
  margin-bottom: 10px;
}

.modal-body h3 {
  font-size: 14px;
  font-weight: 600;
  font-family: 'Poppins', sans-serif;
  color: #333;
  margin-bottom: 5px;
}

.modal-body p {
  font-size: 14px;
  color: #555;
  font-family: 'Inter', sans-serif;
}

.modal-footer {
  display: flex;
  justify-content: center;
  padding: 10px;
}

.close-button {
  background-color: #ff6b6b;
  color: #fff;
  border: none;
  padding: 10px 20px;
  font-size: 14px;
  font-weight: bold;
  cursor: pointer;
  border-radius: 8px;
  transition: background-color 0.3s;
  font-family: 'Inter', sans-serif;
}

.close-button:hover {
  background-color: #ff4a4a;
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes slideUp {
  from {
    transform: translateY(20px);
  }
  to {
    transform: translateY(0);
  }
}
</style>
