<template>
  <div class="register-container">
    <h3>{{ title }}</h3>
    <RegisterInputs @update:form="form = $event" />
  <RegisterButton @click="onCreateAccount" :loading="loading" />
    <div v-if="feedback" style="margin-top:1rem;color:#b00;font-size:1.1rem;">{{ feedback }}</div>
    <div v-if="loading" style="margin-top:0.5rem;">Registering...</div>
  </div>
  <RegisterLinks
    :forgotLink="forgotLink"
    :forgotText="forgotText"
    :registerLink="registerLink"
    :registerText="registerText"
  />
</template>

<script setup>
import { ref } from 'vue';
import axios from 'axios';
import { useRouter } from 'vue-router';
import RegisterInputs from './RegisterInputs.vue';
import RegisterButton from './RegisterButton.vue';
import RegisterLinks from './RegisterLinks.vue';

const props = defineProps({
  title: { type: String, default: 'Account registration' },
  forgotLink: { type: String, default: '#' },
  forgotText: { type: String, default: 'Forgot password?' },
  registerLink: { type: String, default: '/login' },
  registerText: { type: String, default: 'Login' }
});

const form = ref({});
const feedback = ref('');
const loading = ref(false);
const router = useRouter();

async function onCreateAccount() {
  if (loading.value) return;
  feedback.value = '';
  if (!form.value.username || !form.value.email || !form.value.password || !form.value.confirmPassword) {
    feedback.value = 'All fields are required.';
    return;
  }
  if (form.value.password !== form.value.confirmPassword) {
    feedback.value = 'Passwords do not match.';
    return;
  }
  loading.value = true;
  try {
    const res = await axios.post('http://localhost:3000/api/register', {
      username: form.value.username,
      email: form.value.email,
      password: form.value.password,
    });
    // On success, redirect to login with message
    router.push({
      path: '/login',
      query: { msg: res.data.message || 'Registration successful! Please log in.' }
    });
  } catch (err) {
    if (err.response && err.response.data && err.response.data.message) {
      feedback.value = err.response.data.message;
    } else {
      feedback.value = 'Registration failed.';
    }
  } finally {
    loading.value = false;
  }
}
</script>

<style scoped>
.register-container {
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
.register-container h3 {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 2.1rem;
  margin-top: 0.2rem;
  margin-bottom: 1.7rem;
  color: #222;
  letter-spacing: 1px;
}
</style>
