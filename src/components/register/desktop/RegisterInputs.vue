<template>
  <div class="input-container">
    <input type="text" placeholder="username" v-model="username" />
    <input type="email" placeholder="email" v-model="email" />
    <input type="password" placeholder="password" v-model="password" />
    <input type="password" placeholder="Confirm password" v-model="confirmPassword" />
  </div>
</template>

<script setup>
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
.input-container {
  width: 100%;
  display: flex;
  flex-direction: column;
  gap: 1.2rem;
  margin-bottom: 2rem;
}

.input-container input {
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
