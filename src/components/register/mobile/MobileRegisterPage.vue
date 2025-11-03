<template>
  <div class="mobile-register-page">
    <h3 class="mobile-title">{{ props.title }}</h3>

  <RegisterInputs @update:form="form.value = $event" />

  <RegisterButton @click="onCreateAccount" :loading="loading.value" />
    <div
      v-if="feedback.value"
      style="margin-top:1rem;color:#b00;font-size:1.1rem;"
    >
      {{ feedback.value }}
    </div>
  <div v-if="loading.value" style="margin-top:0.5rem;">Registering...</div>

    <RegisterLinks />
  </div>
</template>

<script setup>
import { ref } from 'vue'
import { useRouter } from 'vue-router'
import axios from "axios"

import RegisterInputs from './RegisterInputs.vue'
import RegisterButton from './RegisterButton.vue'
import RegisterLinks from './RegisterLinks.vue'

const props = defineProps({
  title: { type: String, default: 'Account registration' }
})

const router = useRouter()
const form = ref({})
const feedback = ref('')
const loading = ref(false)

async function onCreateAccount() {
  if (loading.value) return;
  feedback.value = '';

  const { username, email, password, confirmPassword } = form.value;

  if (!username || !email || !password || !confirmPassword) {
    feedback.value = 'All fields are required.';
    return;
  }

  if (password !== confirmPassword) {
    feedback.value = 'Passwords do not match.';
    return;
  }

  loading.value = true;

  try {
    const res = await axios.post('http://localhost:3000/api/register', {
      username,
      email,
      password
    });

    feedback.value = res.data.message || 'Registration successful!';
    // router.push('/login') // optional redirect
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
.mobile-register-page {
  max-width: 340px;
  margin: 0 auto;
  padding: 32px 16px;
  background: #ccc;
  border-radius: 16px;
  box-shadow: 0 2px 16px rgba(0, 0, 0, 0.12);
  display: flex;
  flex-direction: column;
  align-items: center;
  border: 2px solid #222;
}

.mobile-title {
  font-family: 'Pixelify Sans', sans-serif;
  font-size: 1.7em;
  margin-top: 0.2rem;
  margin-bottom: 1.5rem;
  color: #222;
  letter-spacing: 1px;
}
</style>
