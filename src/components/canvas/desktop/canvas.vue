<template>
  <div class="canvas-container" :data-active-tool="selectedTool">
    <vue-drawing-canvas
      ref="canvasRef"
      v-model:image="image"
      canvasId="mainCanvas"
      :width="800"
      :height="800"
      :stroke-type="strokeType"
      :line-cap="lineCap"
      :line-join="lineJoin"
      :fill-shape="fillShape"
      :eraser="eraser"
      :lineWidth="line"
      :color="color"
      :background-color="backgroundColor"
      :background-image="backgroundImage"
      :watermark="watermark"
      :initial-image="initialImage"
      saveAs="png"
      :styles="{ border: 'solid 1px #000' }"
      :lock="disabled"
      @mousemove="onMouseMove"
      :additional-images="additionalImages"
    />
  </div>
</template>

<script setup>
import { ref, watch, nextTick } from 'vue'
import VueDrawingCanvas from 'vue-drawing-canvas'

const props = defineProps({
  selectedTool: {
    type: String,
    default: 'drawing',
  },
  // brush size (in pixels) provided by parent
  brushSize: {
    type: Number,
    default: 6,
  },
  // brush color provided by parent
  brushColor: {
    type: String,
    default: '#000000',
  },
})

// ref for the drawing component
const canvasRef = ref(null)

// reactive properties bound to the drawing component (mirror of example)
const image = ref('')
const eraser = ref(false)
const disabled = ref(false)
const fillShape = ref(false)
// internal line width used by the drawing component; initialize from prop
const line = ref(props.brushSize ?? 6)

// keep internal line width in sync when parent changes brushSize
watch(
  () => props.brushSize,
  (v) => {
    if (typeof v === 'number') line.value = v
  },
)

// initialize color from prop and keep in sync
const color = ref(props.brushColor ?? '#000000')
watch(
  () => props.brushColor,
  (v) => {
    if (typeof v === 'string') color.value = v
  },
)
const strokeType = ref('dash')
const lineCap = ref('square')
const lineJoin = ref('miter')
const backgroundColor = ref('#FFFFFF')
const backgroundImage = ref(null)
const watermark = ref(null)
const additionalImages = ref([])
const initialImage = ref([])

function onMouseMove(e) {
  // expose coordinates if needed; keep simple for now
  const coords = canvasRef.value?.getCoordinates?.(e)
  // eslint-disable-next-line no-console
  if (coords) console.log('[CanvasDesktop] coords', coords)
}

// Map incoming toolbar events to drawing actions / modes
watch(
  () => props.selectedTool,
  async (val) => {
    // eslint-disable-next-line no-console
    console.log('[CanvasDesktop] selectedTool ->', val)

    if (!val) return

    switch (val) {
      case 'drawing':
        eraser.value = false
        // keep strokeType as-is or default to freehand
        strokeType.value = 'dash'
        break
      case 'eraser':
        eraser.value = true
        break
      case 'bucket':
        // enable fill mode; the drawing component uses `fill-shape`
        fillShape.value = true
        eraser.value = false
        break
      case 'colorpicker':
        // no built-in UI here; you could open a color picker component instead
        // for now, toggle console hint
        // eslint-disable-next-line no-console
        console.log('[CanvasDesktop] colorpicker selected - open color UI')
        break
      case 'circle':
        eraser.value = false
        fillShape.value = false
        strokeType.value = 'circle'
        break
      case 'line':
        eraser.value = false
        fillShape.value = false
        strokeType.value = 'line'
        break
      case 'square':
        eraser.value = false
        fillShape.value = false
        strokeType.value = 'square'
        break
      case 'undo':
        if (canvasRef.value?.undo) await canvasRef.value.undo()
        break
      case 'redo':
        if (canvasRef.value?.redo) await canvasRef.value.redo()
        break
      case 'clear':
        // prefer reset() to clear everything; redraw() reloads current state
        if (canvasRef.value?.reset) await canvasRef.value.reset()
        break
      default:
        // eslint-disable-next-line no-console
        console.warn('[CanvasDesktop] unknown tool', val)
    }

    // give the child component a tick to react to prop changes
    await nextTick()
  },
)
</script>

<style scoped>
.canvas-container {
  display: flex;
  justify-content: center;
  align-items: center;
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 110vh;
  z-index: 0;
}

canvas {
  background: #fff;
  border-radius: 5px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.3);
  z-index: 1;
}
</style>
