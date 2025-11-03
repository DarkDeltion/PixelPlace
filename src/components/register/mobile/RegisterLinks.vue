<template>
  <div class="mobile-login-links">
    <button class="mobile-link-btn">Forgot Password?</button>
    <button class="mobile-link-btn" @click="router.push('/login')">login</button>
  </div>
</template>

<script setup lang="ts">
import { useRouter } from 'vue-router';
const router = useRouter();
</script>

<style scoped>
.mobile-login-links {
  margin-top: 24px;
  display: flex;
  flex-direction: row;
  justify-content: center;
  gap: 12px;
}
.mobile-link-btn {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 0.95rem;
  background: #e0e0e0;
  color: #222;
  border: 1px solid #222;
  border-radius: 12px;
  padding: 0.5rem 1.2rem;
  cursor: pointer;
  box-shadow: 0 1px 2px rgba(0,0,0,0.07);
  transition: background 0.2s;
}
.mobile-link-btn:active,
.mobile-link-btn:focus {
  background: #d1d1d1;
  outline: none;
}
</style>
