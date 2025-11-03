<template>
  <div class="navbar">
    <NavButtons label="Home" href="/" />

    <div class="site-title">
      <div class="title-animation">
        <h1
          ref="rainbowTitle"
          :class="{ rainbow: isRainbow }"
          @mouseenter="startRainbow"
          @mouseleave="stopRainbow"
        >
          PixelPlace
        </h1>
      </div>
    </div>
    <NavButtons v-if="!currentUser" label="Login" href="/login" />
    <div v-else class="user-dropdown" @mouseenter="showDropdown = true" @mouseleave="showDropdown = false" style="position:relative;">
      <span style="color:#fff;font-size:1.2rem;cursor:pointer;">{{ currentUser }}</span>
      <div v-if="showDropdown" class="dropdown-menu" style="position:absolute;top:2.2rem;right:0;background:#222;border-radius:8px;box-shadow:0 2px 8px rgba(0,0,0,0.18);min-width:140px;z-index:10;">
        <div class="dropdown-item" style="padding:0.7rem 1.2rem;cursor:pointer;color:#fff;" @click="goToAccount">Account Settings</div>
        <div class="dropdown-item" style="padding:0.7rem 1.2rem;cursor:pointer;color:#fff;" @click="logout">Logout</div>
      </div>
    </div>
  </div>
</template>

<script setup>
import NavButtons from './navbuttons.vue'

import { ref } from 'vue'
import { useRouter } from 'vue-router';

const showDropdown = ref(false);
const router = useRouter();

function goToAccount() {
  showDropdown.value = false;
  router.push('/account');
}

function logout() {
  showDropdown.value = false;
  currentUser.value = null;
  router.push('/');
}

const isRainbow = ref(false)

const rainbowTitle = ref(null)

function startRainbow() {
  isRainbow.value = true
}

function stopRainbow() {
  if (rainbowTitle.value) {
    // Get computed color at the end of animation
    const computedColor = getComputedStyle(rainbowTitle.value).color
    // Remove animation class
    isRainbow.value = false
    // Set inline color to current animated color
    rainbowTitle.value.style.color = computedColor
    // Force transition to white
    setTimeout(() => {
      rainbowTitle.value.style.color = '#ffffff'
    }, 10)
    // Remove inline color after transition
    setTimeout(() => {
      rainbowTitle.value.style.color = ''
    }, 1100)
  }
}
</script>

<style>
.navbar {
  width: 100vw;
  height: 125px;
  background-color: #282828;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 17.5vw;
  position: fixed;
  left: 0;
  top: 0;
}
</style>

<style scoped>
.site-title h1 {
  margin: 0;
  font-size: 4rem;
  color: #ffffff;
  transition: color 500ms ease;
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
    rainbowtext 2.5s linear infinite,
    breathing 2s ease-in-out infinite;
}
</style>
