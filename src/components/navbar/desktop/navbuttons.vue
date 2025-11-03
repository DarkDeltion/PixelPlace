<template>
  <router-link :to="href" class="nav-button">
    {{ label }}
  </router-link>
</template>

<script setup>
import { RouterLink } from 'vue-router'
const props = defineProps({
  label: { type: String, required: true }, // text inside the button
  href: { type: String, default: '#' }, // link destination
})
</script>

<style scoped>
.nav-button {
  text-decoration: none;
  color: inherit;
  padding: 0.5rem 1rem;
  font-size: 1.5rem;
  background-color: rgb(90, 90, 90);
  width: 6vw;
  height: 4vh;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 25px;
  transition: 300ms;
}

.nav-button:hover {
  background-color: rgb(110, 110, 110);
  transform: scale(1.1);
  transition: 300ms;
}
</style>
