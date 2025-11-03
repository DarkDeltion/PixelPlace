<template>
  <div class="mobile-login-page">
    <h2 class="mobile-title">Login</h2>
    <LoginInputs />
    <LoginButton />
    <LoginLinks />
  </div>
</template>

<script setup lang="ts">
import LoginInputs from './LoginInputs.vue';
import LoginButton from './LoginButton.vue';
import LoginLinks from './LoginLinks.vue';
// ...existing logic from desktop/LoginPage.vue...
</script>

<style scoped>
.mobile-login-page {
  max-width: 340px;
  margin: 0 auto;
  padding: 32px 16px;
  background: #ccc;
  border-radius: 12px;
  box-shadow: 0 2px 16px rgba(0,0,0,0.08);
  display: flex;
  flex-direction: column;
  align-items: center;
}
.mobile-title {
  font-size: 2em;
  margin-bottom: 18px;
  color: #222;
}
</style>
