<template>
  <div class="mobile-login-inputs">
    <input type="text" placeholder="Username" class="mobile-input" />
    <input type="password" placeholder="Password" class="mobile-input" />
  </div>
</template>

<script setup lang="ts">
// ...existing logic from desktop/LoginInputs.vue...
</script>

<style scoped>
.mobile-login-inputs {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  margin-bottom: 2rem;
}
.mobile-input {
  width: 100%;
  padding: 1.1rem 0;
  border-radius: 18px;
  border: none;
  background: #e0e0e0;
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.25rem;
  text-align: center;
  color: #222;
  outline: none;
  box-shadow: 0 1px 2px rgba(0,0,0,0.07);
}
</style>
