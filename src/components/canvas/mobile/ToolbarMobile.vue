<template>
  <div class="tool-bar">
    <button id="tools" @click="showTools = true">
      <img src="/ToolIcons/drawing-tool.png" alt="Bucket" class="tool-icon" />
      <span class="tool-name">Tools</span>
    </button>
    <button class="colors" @click="showColors = true">
      <img src="/ToolIcons/color%20picker.png" alt="Color Picker" class="tool-icon" />
      <span class="tool-name">Color</span>
    </button>
    <RouterLink to="/">
      <img src="/ToolIcons/undo.png" alt="Home" class="tool-icon" />
      <span class="tool-name">Home</span>
    </RouterLink>
  </div>

  <Tools v-if="showTools" @close="showTools = false" @select="onToolSelect" />
  <Colors v-if="showColors" @close="showColors = false" @select="onColorSelect" />
</template>

<script setup>
import { ref } from 'vue'
import Tools from './Tools.vue'
import Colors from './Colors.vue'

const showTools = ref(false)
const showColors = ref(false)

function onToolSelect(tool) {
  // handle tool selection (placeholder - emits can be connected to parent)
  showTools.value = false
  console.log('selected tool', tool)
}

function onColorSelect(color) {
  // handle color selection
  showColors.value = false
  console.log('selected color', color)
}
</script>

<style scoped>
.tool-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 12px;
  height: 88px; /* slightly smaller for phones */
  background: #1e1e1e;
  padding: 8px 12px; /* give some breathing room */
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 40; /* above canvas and sidebar */
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

/* make interactive elements square and touch-friendly */
.tool-bar > * {
  display: inline-flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 56px; /* target 48-64px tap area */
  height: 56px;
  border-radius: 10px;
  background: #b5b5b5;
  color: #000000;
  text-decoration: none;
  border: none;
  padding: 6px;
  box-sizing: border-box;
  -webkit-tap-highlight-color: transparent;
  margin-left: 20px;
  margin-right: 20px;
}

.tool-bar > *:active {
  background: rgba(255, 255, 255, 0.3);
}

.tool-icon {
  width: 28px;
  height: 28px;
  object-fit: contain;
}

.tool-name {
  display: none; /* hide labels to save space on mobile */
  font-size: 11px;
  margin-top: 4px;
  text-align: center;
}

/* larger screens: show names and increase spacing */
@media (min-width: 400px) {
  .tool-bar {
    gap: 10%;
    height: 96px;
    padding: 2.5% 2.5%;
  }

  .tool-bar > * {
    width: 64px;
    height: 64px;
    border-radius: 12px;
  }

  .tool-name {
    display: block;
  }
}
</style>
