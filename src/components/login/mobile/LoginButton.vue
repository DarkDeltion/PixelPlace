<template>
  <button class="mobile-login-btn">Login</button>
</template>

<script setup lang="ts">
// ...existing logic from desktop/LoginButton.vue...
</script>

<style scoped>
.mobile-login-btn {
  width: 75%;
  padding: 1rem 0;
  border-radius: 18px;
  border: none;
  background: #e0e0e0;
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.25rem;
  color: #222;
  cursor: pointer;
  box-shadow: 0 1px 2px rgba(0,0,0,0.07);
  transition: background 0.2s;
  margin-top: 12px;
}
.mobile-login-btn:hover {
  background: #d1d1d1;
}
</style>
