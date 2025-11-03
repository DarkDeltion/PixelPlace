<template>
  <div class="navbar">
    <div class="site-title">
      <div class="title-animation">
        <h1 ref="rainbowTitle" :class="{ rainbow: isRainbow }" @click="triggerRainbow">
          PixelPlace
        </h1>
      </div>
    </div>
    <HamburgerMenu />
  </div>
</template>

<script setup>
import HamburgerMenu from './hamburgermenu.vue'

import { ref } from 'vue'

const isRainbow = ref(false)
const rainbowTitle = ref(null)

function triggerRainbow() {
  if (isRainbow.value) return
  isRainbow.value = true
  setTimeout(() => {
    isRainbow.value = false
  }, 2500) // match animation duration
}
</script>

<style scoped>
.navbar {
  width: 100vw;
  height: 10vh;
  background-color: #282828;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 20vw;
  position: fixed;
  left: 0;
  top: 0;
  z-index: 100;
}

.site-title h1 {
  margin: 0;
  font-size: clamp(2rem, 8vw, 3.2rem);
  color: #ffffff;
  transition: color 500ms ease;
  letter-spacing: 1px;
}

/* rainbow text animation */
@keyframes rainbowtext {
  0% {
    color: #ffffff;
  }
  10% {
    color: #ff0000;
  }
  20% {
    color: #ff7f00;
  }
  30% {
    color: #ffff00;
  }
  40% {
    color: #00ff00;
  }
  50% {
    color: #00ffff;
  }
  60% {
    color: #0000ff;
  }
  70% {
    color: #7f00ff;
  }
  80% {
    color: #ff00ff;
  }
  90% {
    color: #ffffff;
  }
  100% {
    color: #ffffff;
  }
}

@keyframes breathing {
  0%,
  100% {
    opacity: 1;
    transform: scale(1);
  }
  50% {
    opacity: 0.7;
    transform: scale(1.1);
  }
}

.site-title h1.rainbow {
  animation:
    rainbowtext 2.5s linear 1,
    breathing 2.5s ease-in-out 1;
}

/* @media (max-width: 500px) {
  .navbar {
    height: 48px;
    gap: 2vw;
  }
  .site-title h1 {
    font-size: clamp(1.2rem, 7vw, 2.2rem);
  }
} */
</style>
