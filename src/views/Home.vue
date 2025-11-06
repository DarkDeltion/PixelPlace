<template>
  <!-- navbar -->
  <nav>
    <component :is="width > 750 ? DesktopNavbar : MobileNavbar" />
  </nav>

  <!-- main content -->
  <main>
    <component :is="width > 750 ? desktoplobbieslist : mobilelobbieslist" />
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
  margin-top: 5vw;
  margin-right: 7vw;
  margin-bottom: 5vw;
  margin-left: 7vw;
}
</style>

<script setup>
import desktoplobbieslist from '../components/lobby/desktop/desktoplobbies.vue'
import mobilelobbieslist from '../components/lobby/mobile/mobilelobbies.vue'
import DesktopNavbar from '../components/navbar/desktop/desktopnavbar.vue'
import MobileNavbar from '../components/navbar/mobile/mobilenavbar.vue'

import { ref, onMounted, onUnmounted } from 'vue'

// track screen width
const width = ref(window.innerWidth)
const handleResize = () => {
  width.value = window.innerWidth
}

const testApiConnection = async () => {
  try {
    const res = await fetch('http://localhost:3000/api/test')
    const data = await res.json()
    if (res.ok) {
      console.log('Backend test successful:', data)
    } else {
      console.error('Backend test failed:', data)
    }
  } catch (err) {
    console.error('Backend test error:', err)
  }
}

onMounted(() => {
  window.addEventListener('resize', handleResize)

  testApiConnection()
})

onUnmounted(() => {
  window.removeEventListener('resize', handleResize)
})
</script>
