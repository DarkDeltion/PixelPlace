<template>
  <template v-if="windowWidth > 750">
    <DesktopNavbar @tool-selected="(t) => (selectedTool = t)" />
    <CanvasDesktop :selectedTool="selectedTool" :brushSize="brushSize" :brushColor="brushColor" />
    <Sidebar v-model="brushSize" v-model:color="brushColor" />
  </template>

  <template v-else>
    <ToolbarMobile />
    <MobileCanvas />
  </template>
</template>
<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import Sidebar from '../components/canvas/desktop/sidebar.vue'
import CanvasDesktop from '../components/canvas/desktop/canvas.vue'
import DesktopNavbar from '../components/canvas/desktop/DesktopNavbar.vue'
// mobile
import ToolbarMobile from '../components/canvas/mobile/ToolbarMobile.vue'
import MobileCanvas from '../components/canvas/mobile/MobileCanvas.vue'

const windowWidth = ref(window.innerWidth)

// shared brush size and color between sidebar and canvas
const brushSize = ref(6)
const brushColor = ref('#000000')

// current selected tool from the navbar (shared with desktop canvas)
const selectedTool = ref('drawing')

const handleResize = () => {
  windowWidth.value = window.innerWidth
}

onMounted(() => window.addEventListener('resize', handleResize))
onUnmounted(() => window.removeEventListener('resize', handleResize))
</script>
