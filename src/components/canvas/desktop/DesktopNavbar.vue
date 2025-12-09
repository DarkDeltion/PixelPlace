<template>
  <nav class="tool-bar">
    <ToolButton
      v-for="tool in tools"
      :key="tool.name"
      :name="tool.name"
      :icon="icons[tool.iconKey]"
      :tooltip="tool.tooltip"
      :active="activeTool === tool.name"
      @select="selectTool"
    />
  </nav>
</template>

<script setup>
import { ref } from 'vue'
import ToolButton from './ToolButton.vue'

// Use public/ToolIcons files directly at runtime. Do NOT import from the public folder.
// Build URLs using import.meta.env.BASE_URL so this works when the app is served from a subpath.
const base = import.meta.env.BASE_URL ?? '/'

const toolFiles = {
  DrawingIcon: 'drawing-tool.png',
  EraserIcon: 'eraser.png',
  BucketIcon: 'bucket tool.png',
  ColorPickerIcon: 'color picker.png',
  CircleIcon: 'circle tool.png',
  LineIcon: 'line tool.png',
  SquareIcon: 'square tool.png',
  UndoIcon: 'undo.png',
  RedoIcon: 'redo.png',
  ClearIcon: 'grid tool.png',
}

const encode = (s) => encodeURIComponent(s)

const icons = {}
for (const [key, file] of Object.entries(toolFiles)) {
  icons[key] = `${base}ToolIcons/${encode(file)}`
}

// list of tools rendered in the toolbar (maps to keys in `icons`)
const tools = [
  { name: 'drawing', iconKey: 'DrawingIcon', tooltip: 'Drawing' },
  { name: 'eraser', iconKey: 'EraserIcon', tooltip: 'Eraser' },
  { name: 'circle', iconKey: 'CircleIcon', tooltip: 'Circle' },
  { name: 'line', iconKey: 'LineIcon', tooltip: 'Line' },
  { name: 'square', iconKey: 'SquareIcon', tooltip: 'Square' },
  { name: 'undo', iconKey: 'UndoIcon', tooltip: 'Undo' },
  { name: 'redo', iconKey: 'RedoIcon', tooltip: 'Redo' },
  { name: 'clear', iconKey: 'ClearIcon', tooltip: 'Clear' },
]

// reactive UI state: which tool is active
const activeTool = ref('drawing')

// emit events to parent components when a tool is selected
const emit = defineEmits(['tool-selected'])

// tools that perform an immediate action and should not toggle active state
const actionTools = new Set(['undo', 'redo', 'clear'])

function selectTool(name) {
  // always notify parent
  emit('tool-selected', name)

  // only set active state for persistent tools (drawing, eraser, shapes, etc.)
  if (!actionTools.has(name)) {
    activeTool.value = name
  }
}
</script>

<style>
.tool-bar {
  display: flex;
  justify-content: center;
  align-items: center;
  gap: 10px;
  height: 100px;
  background: #1e1e1e;
  padding: 0 20px;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 40;
  box-shadow: 0 2px 10px rgba(0, 0, 0, 0.2);
}

.tool-btn {
  position: relative;
  width: 64px;
  height: 64px;
  border: none;
  background: #2a2a2a;
  border-radius: 12px;
  cursor: pointer;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  transition:
    transform 0.15s ease,
    background 0.2s ease,
    box-shadow 0.2s ease;
  box-shadow: 0 2px 4px rgba(0, 0, 0, 0.25);
}

.tool-btn:hover {
  background: #333;
  transform: translateY(-4px);
}

.tool-btn.active {
  background: #3a86ff;
  box-shadow: 0 0 12px rgba(58, 134, 255, 0.6);
}

.tooltip {
  position: absolute;
  bottom: -32px;
  left: 50%;
  transform: translateX(-50%) scale(0.9);
  background: #111;
  color: #fff;
  padding: 4px 10px;
  border-radius: 6px;
  font-size: 12px;
  white-space: nowrap;
  opacity: 0;
  pointer-events: none;
  transition:
    opacity 0.2s,
    transform 0.2s;
}

.tool-btn:hover .tooltip {
  opacity: 1;
  transform: translateX(-50%) scale(1);
}

.tool-icon {
  width: 26px;
  height: 26px;
  display: block;
  object-fit: contain;
  background: #ffffff72;
  padding: 8px;
  border-radius: 50%;
  box-shadow: inset 0 1px 2px rgba(0, 0, 0, 0.3);
}
</style>
