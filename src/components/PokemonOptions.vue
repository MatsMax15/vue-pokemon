<template>
	<div class="options-container">
		<div class="option" v-for="pokemon in pokemons" :key="pokemon.id" :id="pokemon.id">
			<button type="button" @click="selection(pokemon.id)" :disabled="isDisabled">{{ pokemon.name }}</button>
		</div>
	</div>
</template>

<script>
export default {
	props: {
		pokemons: {
			type: Array,
			required: true,
		},
	},
	name: 'Component-Options',
	data() {
		return {
			isDisabled: false,
            isActive: null
		}
	},
	methods: {
		selection(pokemonId) {
            this.isDisabled = true
			this.$emit('selection', pokemonId)
            
            const element = document.getElementById(pokemonId).querySelector('button')
            element.classList.add('active')
		},
	},
}
</script>

<style scoped>
.option {
	padding: 10px;
}

.option button {
	background-color: #ffcc01;
	border-radius: 5px;
	border: none;
	box-shadow: 0 0 2px 2px var(--color-secondary);
	color: var(--color-secondary);
	cursor: pointer;
	font-size: 1.5rem;
	font-weight: 600;
	height: 70px;
	opacity: 0.8;
	padding: 10px;
	text-transform: capitalize;
	transition: 0.3s;
	width: 80%;
}

.option button:hover {
	box-shadow: 0 0 4px 2px var(--color-secondary);
	opacity: 1;
}

.option button.active {
    background: #ffcc01 !important;
}

.options-container {
	align-items: center;
	display: grid;
	grid-template-columns: repeat(2, 2fr);
	justify-content: center;
	width: 100%;
}

@media (max-width: 1080px) {
	.options-container {
		gap: 10px;
		grid-template-columns: repeat(2, 2fr);
		width: 100%;
	}
}

@media (max-width: 540px) {
	.options-container {
		gap: 10px;
	}

	.option {
		margin-top: 0px;
	}

	.option button {
		width: 100%;
	}
}

@media (max-width: 440px) {
    .option button {
        font-size: 1.5rem;
        min-height: 40px;
        padding: 5px;
    }
}
</style>
