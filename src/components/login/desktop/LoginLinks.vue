<template>
	<div class="login-links">
		<a :href="forgotLink">{{ forgotText }}</a>
		<span class="separator">|</span>
		<a :href="registerLink">{{ registerText }}</a>
	</div>
</template>
<script setup>
defineProps({
	forgotLink: { type: String, default: '#' },
	forgotText: { type: String, default: 'Forgot password?' },
	registerLink: { type: String, default: '#' },
	registerText: { type: String, default: 'account register' }
})
</script>
<style>
		.login-links {
			margin-top: 0.7rem;
			text-align: center;
			width: 100%;
			font-family: 'Pixelify Sans', sans-serif;
			color: #fff;
			font-size: 0.95rem;
		}

		.login-links a {
			font-family: 'Pixelify Sans', sans-serif;
			color: #fff;
			font-size: 0.95rem;
			text-decoration: none;
			margin: 0 0.2rem;
		}
		.login-links a:hover {
			text-decoration: underline;
		}
        
        .separator {
		color: #fff;
		margin: 0 0.3rem;
		font-size: 0.95rem;
		vertical-align: middle;
		user-select: none;
	}
</style>
