<template>
  <template v-if="windowWidth > 750">
    <DesktopNavbar />
    <CanvasDesktop />
    <Sidebar />
  </template>

  <template v-else>
    <ToolbarMobile />
    <MobileCanvas />
  </template>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from 'vue'

// desktop
import Sidebar from '../components/canvas/desktop/sidebar.vue'
import CanvasDesktop from '../components/canvas/desktop/canvas.vue'
import DesktopNavbar from '../components/canvas/desktop/DesktopNav.vue'
// mobile
import ToolbarMobile from '../components/canvas/mobile/ToolbarMobile.vue'
import MobileCanvas from '../components/canvas/mobile/MobileCanvas.vue'

const windowWidth = ref(window.innerWidth)

const handleResize = () => {
  windowWidth.value = window.innerWidth
}

onMounted(() => window.addEventListener('resize', handleResize))
onUnmounted(() => window.removeEventListener('resize', handleResize))
</script>
