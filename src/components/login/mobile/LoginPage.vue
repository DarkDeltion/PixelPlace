<template>
  <div class="mobile-login-page">
    <h2 class="mobile-title">Login</h2>
    <LoginInputs />
    <LoginButton />
  </div>
  <LoginLinks />
</template>

<script setup lang="ts">
import LoginInputs from './LoginInputs.vue';
import LoginButton from './LoginButton.vue';
import LoginLinks from './LoginLinks.vue';
// ...existing logic from desktop/LoginPage.vue...
</script>

<style scoped>
.mobile-login-page {
  background: #ccc;
  border-radius: 24px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.22);
  padding: 1.6rem 1.2rem 1.2rem 1.2rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 240px;
  max-width: 340px;
  border: 2px solid #222;
  margin: 0 auto 16px auto;
}
.mobile-title {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 2em;
  margin-top: 0.2rem;
  margin-bottom: 1.7rem;
  color: #222;
  letter-spacing: 1px;
}
</style>
