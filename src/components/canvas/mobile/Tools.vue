<template>
  <div class="overlay" @click.self="close">
    <div class="panel">
      <header class="panel-header">
        <h3>Tools</h3>
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

      <div class="tool-grid">
        <button
          v-for="t in tools"
          :key="t.key"
          class="tool-item"
          @click="select(t.key)"
          type="button"
        >
          <img :src="t.src" :alt="t.label" />
          <span>{{ t.label }}</span>
        </button>
      </div>
    </div>
  </div>
</template>

<script setup>
const emit = defineEmits(['close', 'select'])

const tools = [
  { key: 'bucket', label: 'Bucket', src: '/ToolIcons/bucket%20tool.png' },
  { key: 'circle', label: 'Circle', src: '/ToolIcons/circle%20tool.png' },
  { key: 'picker', label: 'Color Picker', src: '/ToolIcons/color%20picker.png' },
  { key: 'draw', label: 'Drawing', src: '/ToolIcons/drawing-tool.png' },
  { key: 'eraser', label: 'Eraser', src: '/ToolIcons/eraser.png' },
  { key: 'grid', label: 'Grid', src: '/ToolIcons/grid%20tool.png' },
  { key: 'line', label: 'Line', src: '/ToolIcons/line%20tool.png' },
  { key: 'square', label: 'Square', src: '/ToolIcons/square%20tool.png' },
]

function close() {
  emit('close')
}

function select(key) {
  emit('select', key)
}
</script>

<style scoped>
.overlay {
  position: fixed;
  inset: 0;
  background: rgba(0, 0, 0, 0.5);
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
  padding: 12px;
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
  margin-bottom: 8px;
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

.tool-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 8px;
}

.tool-item {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 6px;
  background: #2b2b2b;
  border-radius: 10px;
  padding: 10px;
  color: #fff;
  border: none;
}

.tool-item img {
  width: 28px;
  height: 28px;
  object-fit: contain;
  background: #fff;
  padding: 6px;
  border-radius: 8px;
}

.tool-item:active {
  transform: translateY(1px);
  filter: brightness(1.05);
}

@media (min-width: 640px) {
  .panel {
    border-radius: 10px;
    margin-bottom: 24px;
  }

  .tool-grid {
    grid-template-columns: repeat(6, 1fr);
  }
}
</style>
