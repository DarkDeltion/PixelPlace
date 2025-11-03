<template>
	<div class="button-container">
		<button type="submit">Login</button>
	</div>
</template>
<style>
		.button-container {
			width: 100%;
			display: flex;
			justify-content: center;
			margin-bottom: 0.5rem;
		}

		.button-container button {
			width: 75%;
			padding: 1rem 0;
			border-radius: 18px;
			border: none;
			background: #e0e0e0;
			font-family: 'Pixelify Sans', sans-serif;
			font-size: 1.25rem;
			color: #222;
			cursor: pointer;
			box-shadow: 0 1px 2px rgba(0,0,0,0.07);
			transition: background 0.2s;
		}
		.button-container button:hover {
			background: #d1d1d1;
		}
</style>
