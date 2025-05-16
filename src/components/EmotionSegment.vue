<template>
  <g @click="handleClick" class="segment-group">
    <!-- Сегмент -->
    <path :d="pathData" :fill="color" class="segment" />

    <!-- Текст -->
    <text
      :x="textPosition.x"
      :y="textPosition.y"
      text-anchor="middle"
      dominant-baseline="middle"
      class="segment-text"
    >
      {{ label }}
    </text>
  </g>
</template>

<script setup>
import { defineProps, defineEmits, computed } from 'vue'

const props = defineProps({
  startAngle: Number,
  endAngle: Number,
  radius: Number,
  color: String,
  label: String,
  emotion: Object,
})

const emit = defineEmits(['select'])

const handleClick = () => {
  emit('select', props.emotion)
}

/**
 * Конвертируем угол в координаты
 */
const polarToCartesian = (cx, cy, radius, angle) => {
  const radians = (angle - 90) * (Math.PI / 180)
  return {
    x: cx + radius * Math.cos(radians),
    y: cy + radius * Math.sin(radians),
  }
}

/**
 * Генерация path для сектора
 */
const describeArc = (x, y, radius, startAngle, endAngle) => {
  const start = polarToCartesian(x, y, radius, endAngle)
  const end = polarToCartesian(x, y, radius, startAngle)
  const largeArcFlag = endAngle - startAngle <= 180 ? '0' : '1'

  return [
    `M ${start.x} ${start.y}`,
    `A ${radius} ${radius} 0 ${largeArcFlag} 0 ${end.x} ${end.y}`,
    `L ${x} ${y}`,
    'Z',
  ].join(' ')
}

const pathData = computed(() =>
  describeArc(200, 200, props.radius, props.startAngle, props.endAngle),
)

/**
 * Координаты для текста
 */
const textPosition = computed(() => {
  const angle = (props.startAngle + props.endAngle) / 2
  return polarToCartesian(200, 200, props.radius / 1.5, angle)
})
</script>

<style scoped>
.segment-group {
  cursor: pointer;
  transition:
    fill 0.3s,
    filter 0.3s;
}

.segment {
  transition:
    fill 0.3s,
    filter 0.3s;
}

.segment-group:hover .segment {
  fill-opacity: 0.8;
  filter: drop-shadow(0px 0px 5px rgba(0, 0, 0, 0.5));
}

.segment-text {
  fill: #ffffff;
  font-weight: bold;
  font-size: 14px;
}
</style>
