<template>
  <button class="tool-btn" :class="{ active: active }" @click="handleClick">
    <span class="img">
      <img class="tool-icon" :src="icon" :alt="tooltip" />
    </span>
    <span class="tooltip">{{ tooltip }}</span>
  </button>
</template>

<script setup>
const props = defineProps({
  name: { type: String, required: true },
  icon: { type: String, required: true },
  tooltip: { type: String, required: true },
  active: { type: Boolean, default: false },
})

const emit = defineEmits(['select'])

function handleClick() {
  emit('select', props.name)
}
</script>

<!-- No local styles; reuse the navbar's global styles for consistency -->
