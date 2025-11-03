<template>
  <div class="login-container">
    <h3>Login</h3>
    <div v-if="msg" style="margin-bottom:1rem;color:#080;font-size:1.1rem;">{{ msg }}</div>
    <LoginInputs />
    <LoginButton />
  </div>
  <LoginLinks 
    forgotLink="/forgotpassword" 
    forgotText="Forgot password?" 
    registerLink="/register" 
    registerText="Create account" 
  />
</template>

<script setup>
import LoginInputs from './LoginInputs.vue';
import LoginButton from './LoginButton.vue';
import LoginLinks from './LoginLinks.vue';

import { useRoute } from 'vue-router';
const route = useRoute();
const msg = route.query.msg;
</script>

<style>
.login-container {
  background: #ccc;
  border-radius: 24px;
  box-shadow: 0 4px 16px rgba(0,0,0,0.22);
  padding: 1.6rem 3.5rem 2.5rem 3.5rem;
  display: flex;
  flex-direction: column;
  align-items: center;
  min-width: 400px;
  max-width: 480px;
  border: 2px solid #222;
}
.login-container h3 {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 2.1rem;
  margin-top: 0.2rem;
  margin-bottom: 1.7rem;
  color: #222;
  letter-spacing: 1px;
}
</style>