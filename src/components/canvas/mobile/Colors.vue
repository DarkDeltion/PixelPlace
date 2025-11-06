<template>
  <div class="overlay" @click.self="close">
    <div class="panel">
      <header class="panel-header">
        <h3>Colors</h3>
        <button class="close-btn" @click="close" aria-label="Close">
          <svg
            width="18"
            height="18"
            viewBox="0 0 24 24"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            aria-hidden
          >
            <path
              d="M18 6L6 18"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
            <path
              d="M6 6L18 18"
              stroke="currentColor"
              stroke-width="2"
              stroke-linecap="round"
              stroke-linejoin="round"
            />
          </svg>
        </button>
      </header>

      <!-- picker on top -->
      <div class="color-wheel" @pointerdown.prevent="pickFromWheel($event)"></div>

      <!-- presets pinned to bottom of panel -->
      <div class="presets-row">
        <div class="presets">
          <button
            v-for="c in presetColors"
            :key="c"
            class="swatch"
            :style="{ background: c }"
            @click="select(c)"
            :aria-label="c"
          ></button>
        </div>
      </div>

      <div class="actions">
        <button class="apply-btn" @click="close">Done</button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['close', 'select'])

const presetColors = [
  '#ff4d4d',
  '#ff944d',
  '#ffd54d',
  '#4dff4d',
  '#4dffff',
  '#4d4dff',
  '#b84dff',
  '#ff4dd2',
  '#ffffff',
  '#000000',
]

function close() {
  emit('close')
}

function select(color) {
  emit('select', color)
}

function pickFromWheel(e) {
  // placeholder: pick a color based on pointer position for now
  // map x position to hue as a simple approximation
  const rect = e.currentTarget.getBoundingClientRect()
  const x = e.clientX - rect.left
  const hue = Math.round((x / rect.width) * 360)
  const color = `hsl(${hue} 85% 55%)`
  emit('select', color)
}
</script>

<style scoped>
.overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.45);
  display: flex;
  align-items: flex-end;
  justify-content: center;
  z-index: 60;
}

.panel {
  width: 100%;
  max-width: 720px;
  background: #1e1e1e;
  border-radius: 12px;
  padding: 14px;
  box-shadow: 0 8px 24px rgba(0, 0, 0, 0.4);
  margin-bottom: 100px; /* keep above toolbar */
  max-height: calc(100vh - 140px);
  overflow: auto;
}

.panel-header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  color: #fff;
  margin-bottom: 12px;
}

.close-btn {
  background: rgba(255, 255, 255, 0.03);
  border: none;
  color: #fff;
  width: 36px;
  height: 36px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  border-radius: 8px;
  transition:
    background 120ms ease,
    transform 120ms ease;
}

.color-wheel {
  width: 100%;
  height: 220px;
  border-radius: 12px;
  background: conic-gradient(red, yellow, lime, cyan, blue, magenta, red);
  position: relative;
  box-shadow: 0 6px 18px rgba(0, 0, 0, 0.35);
  margin-bottom: 12px;
}

.presets-row {
  display: flex;
  justify-content: center;
  padding: 8px 0 4px;
}

.presets {
  display: flex;
  gap: 8px;
  flex-wrap: wrap;
  justify-content: center;
}

.swatch {
  width: 44px;
  height: 44px;
  border-radius: 8px;
  border: 2px solid rgba(255, 255, 255, 0.06);
  box-shadow: 0 2px 6px rgba(0, 0, 0, 0.25);
  border: 3px solid rgb(255, 255, 255);
}

.actions {
  margin-top: 12px;
  display: flex;
  justify-content: center;
}
.apply-btn {
  background: linear-gradient(180deg, #3a3a3a, #222);
  border: none;
  color: #fff;
  padding: 10px 18px;
  border-radius: 14px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.35);
}

@media (min-width: 640px) {
  .panel {
    max-width: 540px;
  }
  .color-wheel {
    height: 200px;
  }
}
</style>
