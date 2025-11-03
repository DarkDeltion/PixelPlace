<template>
  <nav>
    <component :is="width > 750 ? DesktopNavbar : MobileNavbar" />
  </nav>

  <main>
    <component :is="width > 750 ? DesktopLoginPage : MobileLoginPage" />
  </main>
</template>

<style scoped>


nav {
  width: 100vw;
  height: 10vh;
  font-family: 'Pixelify Sans', sans-serif;
  color: white;
}

main {
  min-height: 75vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}
</style>

<script setup>
import DesktopNavbar from '../components/navbar/desktop/desktopnavbar.vue'
import MobileNavbar from '../components/navbar/mobile/mobilenavbar.vue'
import DesktopLoginPage from '../components/login/desktop/DesktopLoginPage.vue'
import MobileLoginPage from '../components/login/mobile/MobileLoginPage.vue'
import { ref, onMounted, onUnmounted } from 'vue'

// track screen width
const width = ref(window.innerWidth)

const handleResize = () => {
  width.value = window.innerWidth
}

onMounted(() => {
  window.addEventListener('resize', handleResize)
})
</script>
