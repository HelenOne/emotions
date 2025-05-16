<template>
  <div class="circle-container">
    <svg width="400" height="400">
      <EmotionSegment
        v-for="(emotion, index) in emotions"
        :key="index"
        :startAngle="calculateStartAngle(index)"
        :endAngle="calculateEndAngle(index)"
        :radius="180"
        :color="emotion.color"
        :label="emotion.emoji ? emotion.emoji : emotion.name"
        :emotion="emotion"
        @select="handleSelect"
      />
    </svg>

    <EmotionModal
      v-if="selectedEmotion"
      :emotion="selectedEmotion"
      @close="selectedEmotion = null"
    />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import EmotionSegment from './EmotionSegment.vue'
import EmotionModal from './EmotionModal.vue'
import emotionsData from '../assets/emotions.json'

const emotions = ref(emotionsData)

const selectedEmotion = ref(null)

const handleSelect = (emotion) => {
  selectedEmotion.value = emotion
}

const calculateStartAngle = (index) => {
  return (360 / emotions.value.length) * index
}

const calculateEndAngle = (index) => {
  return (360 / emotions.value.length) * (index + 1)
}
</script>

<style scoped>
.circle-container {
  width: 400px;
  height: 400px;
  position: relative;
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
