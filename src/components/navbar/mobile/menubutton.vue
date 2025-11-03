<template>
  <router-link :to="href" class="menu-link" @click.native="onClick">
    <slot />
  </router-link>
</template>

<script setup>
import { RouterLink } from 'vue-router'
const props = defineProps({
  href: {
    type: String,
    default: '#',
  },
})
const emit = defineEmits(['click'])
function onClick(e) {
  emit('click', e)
}
</script>

<style scoped>
.menu-link {
  display: block;
  width: 90%;
  box-sizing: border-box;
  padding: 3vh;
  text-align: center;
  font-size: 1.25rem;
  color: #fff;
  background: rgba(40, 40, 40, 0.95);
  border: none;
  border-radius: 12px;
  transition: background 0.2s;
  text-decoration: none;
  cursor: pointer;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10px;
  margin-bottom: 10px;
}
.menu-link:active,
.menu-link:hover {
  background: rgba(60, 60, 60, 1);
}
</style>
