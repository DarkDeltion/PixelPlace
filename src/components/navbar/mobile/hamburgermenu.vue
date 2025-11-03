<template>
  <div class="hamburger-menu" @click="toggleMenu">
    <div :class="{ open: isOpen }" class="bars">
      <div class="bar"></div>
      <div class="bar"></div>
      <div class="bar"></div>
    </div>
    <transition name="dropdown-fade">
      <div v-if="isOpen" class="menu-dropdown">
        <MenuButton href="/" @click="closeMenu">Home</MenuButton>
        <MenuButton href="/login" @click="closeMenu">Login</MenuButton>
      </div>
    </transition>
  </div>
</template>

<script setup>
import { ref } from 'vue'
import MenuButton from './menubutton.vue'

const isOpen = ref(false)
function toggleMenu() {
  isOpen.value = !isOpen.value
}
function closeMenu() {
  isOpen.value = false
}
</script>

<style scoped>
.hamburger-menu {
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
  cursor: pointer;
}

.bars {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  width: 40px;
  height: 40px;
}

.bar {
  width: 100%;
  height: 6px;
  background-color: #ffffff;
  margin: 4px 0;
  transition: all 0.3s ease;
}

.menu-dropdown {
  position: fixed;
  top: 9.5vh; /* or adjust to your navbar height */
  left: 0;
  right: 0;
  background: rgba(30, 30, 30, 0.97);
  backdrop-filter: blur(10px);
  border-radius: 0 0 18px 18px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.2);
  width: 100vw;
  max-width: 100vw;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  align-items: stretch;
  padding: 12px 0;
  box-sizing: border-box;
}

/* Dropdown animation */
.dropdown-fade-enter-active,
.dropdown-fade-leave-active {
  transition:
    opacity 0.35s cubic-bezier(0.4, 0, 0.2, 1),
    transform 0.35s cubic-bezier(0.4, 0, 0.2, 1);
}
.dropdown-fade-enter-from,
.dropdown-fade-leave-to {
  opacity: 0;
  transform: translateY(-16px) scaleY(0.98);
}
.dropdown-fade-enter-to,
.dropdown-fade-leave-from {
  opacity: 1;
  transform: translateY(0) scaleY(1);
}
</style>
