<template>
  <div class="mobile-login-inputs">
    <input type="text" placeholder="Username" class="mobile-input" v-model="username" />
    <input type="email" placeholder="Email" class="mobile-input" v-model="email" />
    <input type="password" placeholder="Password" class="mobile-input" v-model="password" />
    <input type="password" placeholder="Confirm password" class="mobile-input" v-model="confirmPassword" />
  </div>
</template>

<script setup lang="ts">
import { ref, watch, defineEmits } from 'vue';
const emit = defineEmits(['update:form']);

const username = ref('');
const email = ref('');
const password = ref('');
const confirmPassword = ref('');

watch([username, email, password, confirmPassword], () => {
  emit('update:form', {
    username: username.value,
    email: email.value,
    password: password.value,
    confirmPassword: confirmPassword.value,
  });
});
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
