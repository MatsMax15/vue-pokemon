<script>
import PokemonPage from '@/pages/PokemonPage.vue'
// import Loading from '@/components/Loading'

export default {
	name: 'App',
	components: {PokemonPage},
  methods: {
    selectedTheme(e) {
      const tag = e.nodeName
      const element = tag === 'BUTTON' ? e.target : e.target.closest('button')
      element.classList.toggle('light')
      element.classList.toggle('dark')
      
      const body = document.querySelector('body')
      body.classList.toggle('light')
      body.classList.toggle('dark')
    }
  }
}
</script>

<template>
  <button @click="selectedTheme" type="button" class="theme dark">
    <span>
      <img class="img-dark" src="https://cdn-icons-png.flaticon.com/512/3026/3026346.png" alt="">
      <img class="img-light" src="https://cdn-icons-png.flaticon.com/512/3026/3026409.png" alt="">
    </span>
  </button>

	<pokemon-page />
</template>

<style>
  #app {
    -moz-osx-font-smoothing: grayscale;
    -webkit-font-smoothing: antialiased;
    margin: 0;
    padding: 0;
    text-align: center;
    height: 100%;
  }
  
  .theme {
    background: transparent;
    border: none;
    position: absolute;
    top: 10px;
    right: 10px;
    border: solid 1px rgb(192, 191, 191);
    border-radius: 60px;
    width: 80px;
    background: rgb(235, 235, 235);
    height: 40px;
    cursor: pointer;
    transition: 0.3s;
    box-shadow: none;
  }
  
  .theme span {
    position: absolute;
    top: 3px;
    left: 3px;
    background: #fff;
    height: 30px;
    width: 30px;
    border-radius: 50%;
    display: flex;
    justify-content: center;
    align-items: center;
    border: solid 1px rgb(192, 191, 191);
    transition: 0.3s;
  }
  
  .theme.dark span {
    transform: translateX(40px);
  }
  
  .theme.dark {
    background: rgb(33, 37, 58);
  }
  
  .theme.light .img-light {
    opacity: 1;
  }
  
  .theme.light .img-dark {
    opacity: 0;
  }
  
  .theme.dark .img-light {
    opacity: 0;
  }
  
  .theme.dark .img-dark {
    opacity: 1;
  }
  
  .theme img {
    width: 25px;
    filter: brightness(0);
    position: absolute;
    transition: 0.3s;
  }
  </style>