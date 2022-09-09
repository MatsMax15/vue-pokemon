<template>
	<div class="title">
		<h1>Quien es este</h1>
		<img src="@/assets/img/logo.png" alt="">
		<h1>???</h1>
	</div>
</template>

<script>
export default {

}
</script>

<style scoped>
	.title {
		display: block;
		margin-top: 20px;
	}

	h1 {
		padding: 0;
		margin: 0;
		font-size: 2rem;
	}

	img {
		width: 200px;
	}

	@media (max-width: 440px) {
		h1 {
			font-size: 1.5rem;
		}

		img {
			width: 120px;
		}
	}
</style>