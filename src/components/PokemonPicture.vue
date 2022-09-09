<template>
	<div class="pokemon-container">
		<img src="@/assets/img/Pokeball.png" alt="pokeball" class="pokeball">

		<img class="hidden-pokemon" :src="imgSrc" alt="pokemon" />

		<img v-if="showPokemon" class="fade-in" :src="imgSrc" alt="pokemon" />
	</div>
</template>

<script>

export default {
	props: {
		pokemonId: {
			type: Number,
			required: true,
			defaul: 1
		},
		showPokemon: {
			type: Boolean,
			required: true,
			defaul: false
		}
	},
	name: 'Component-Picture',
	computed: {
		imgSrc() {
			return `https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/${ this.pokemonId }.svg`
		}
	}
}
</script>

<style scoped>
.hidden-pokemon {
	filter: brightness(0);
}

.pokemon-container {
	height: 250px;
	display: flex;
	justify-content: center;
	align-items: center;
	margin-bottom: 10px;
}

.pokeball {
	position: absolute;
	width: 250px;
	height: 250px;
}

img {
	height: 200px;
	position: absolute;
	user-select: none;
	-moz-user-select: none;
	-ms-user-select: none;
	-webkit-user-drag: none;
	-webkit-user-select: none;
}

@media (max-width: 440px) {
	.pokemon-container {
		height: 180px;
	}

	.pokeball {
		width: 150px;
		height: 150px;
	}

	img {
		width: 180px;
	}
}
</style>
