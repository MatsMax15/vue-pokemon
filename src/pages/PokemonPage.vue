<template>
	<loading v-if="!pokemon" />
	<h1 v-if="!pokemon">Espere por favor...</h1>

	<div v-else>
		<pokemon-head />

		<!-- TODO: img -->
		<pokemon-picture :pokemon-id="pokemon.id" :show-pokemon="showPokemon" />
		<!-- TODO: Options -->
		<pokemon-options :pokemons="pokemonArr" @selection="checkAnswer" />

		<div class="message-container" v-if="showAnswer">
			<div class="left-container">
				<img :src="imgMsg" alt="">
			</div>
			<div class="right-container">
				<h2>{{ message }}</h2>
				<button @click="newGame">Siguiente</button>
			</div>
		</div>
	</div>
</template>

<script>
import PokemonPicture from '@/components/PokemonPicture.vue'
import PokemonOptions from '@/components/PokemonOptions.vue'
import PokemonHead from '@/components/PokemonHeader.vue'

import Loading from '@/components/Loading.vue'

import getPokemonOptions from '@/pages/helpers/getPokemonOptions'

export default {
	name: 'Container-Pokemon',
	components: { PokemonPicture, PokemonOptions, PokemonHead, Loading },
	data() {
		return {
			pokemonArr: [],
			pokemon: null, 
			showPokemon: false,
			showAnswer: false,
			message: '',
			imgMsg: ''
		}
	},
	methods: {
		async mixPokemonArray() {
			this.pokemonArr = await getPokemonOptions()

			const rndInt = Math.floor( Math.random() * 4 )
			this.pokemon = this.pokemonArr[ rndInt ]
		},
		checkAnswer(selectedId) {
			this.showPokemon = true
			this.showAnswer = true

			if ( selectedId === this.pokemon.id ) {
				this.imgMsg = 'https://i0.wp.com/eltallerdehector.com/wp-content/uploads/2022/06/6420b-pikachu-sentado-png.png?resize=450%2C450&ssl=1'
				this.message = `Correcto, ${ this.pokemon.name }`
			}
			else {
				this.message = `Oops, era ${ this.pokemon.name }`
				this.imgMsg = 'https://www.pngmart.com/files/12/Charizard-PNG-Picture.png'
			}
		},
		newGame() {
			
			this.showPokemon = false
			this.showAnswer = false
			this.pokemonArr = []
			this.pokemon = null
			this.mixPokemonArray()

		}
	},
	mounted() {
		this.mixPokemonArray()
	}
}
</script>

<style scoped>
.message-container {
	margin-top: 20px;
	margin-bottom: 50px;
	display: flex;
	justify-content: space-between;
}

.message-container h2 {
	font-size: 3rem;
	text-transform: capitalize;
}

.left-container,
.right-container {
	width: 50%;
	display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center;
}

.message-container img {
	height: 250px;
}

button {
	background: #eee;
	border-radius: 5px;
	border: none;
	font-size: 2rem;
	padding: 15px;
	background: #25857d;
	width: 400px;
	color: #fff;
}

@media (max-width: 540px) {
	.message-container {
		flex-direction: column;
	}

	.left-container {
		height: 100px;
	}

	.message-container img {
		height: 100px;
	}

	.left-container,
	.right-container {
		width: 100%;
	}

	.message-container h2 {
		font-size: 1.5rem;
		margin: 10px;
	}

	button {
		width: calc(100% - 20px);
	}
}
</style>