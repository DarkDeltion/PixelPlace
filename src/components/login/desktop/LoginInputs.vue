<template>
    <form class="input-container" @submit.prevent="onSubmit">
        <input v-model="username" type="text" placeholder="Username" autocomplete="username" />
        <input v-model="password" type="password" placeholder="Password" autocomplete="current-password" />
    </form>
</template>>

<script setup>
import { ref } from 'vue';
import { useRouter } from 'vue-router';
const username = ref('');
const password = ref('');
const loading = ref(false);

const emit = defineEmits(['login']);
const router = useRouter();

async function onSubmit() {
	if (loading.value) return;
	loading.value = true;
	try {
		const response = await fetch('http://localhost:3000/api/login', {
			method: 'POST',
			headers: { 'Content-Type': 'application/json' },
			body: JSON.stringify({ username: username.value, password: password.value })
		});
		const data = await response.json();
		if (response.ok) {
			emit('login', data);
			currentUser.value = username.value;
			router.push('/'); // Redirect to home page
		} else {
			alert(data.message || 'Login failed');
		}
	} catch (err) {
		alert('Network error');
	} finally {
		loading.value = false;
	}
}
</script>
<style>
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
