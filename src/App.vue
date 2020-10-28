<template>
  <h1 class="pokedex">Pokedex</h1>
  <PokeList 
    v-bind:pokemonsData='pokemonsData' 
    v-bind:loading="loading"
  />
  <div class="bttns constrict">

    <button type="button" @click="prevPage"> Prev. </button>
    <button type="button" @click="nextPage"> Next </button>
  </div>

  <footer>
    <p>Created with <a href="https://vuejs.org/">Vuejs</a> by <a href="https://github.com/mnegabriel">Gabriel Dantas</a></p>
  </footer>
</template>


<script>
import PokeList from './components/PokeList'
import axios from 'axios'

export default {
  name: 'App',
  components: {
    PokeList
  },
  data() {
    return {
      apiUrl: 'https://pokeapi.co/api/v2/pokemon?limit=9',
      next: '',
      previous: '',
      pokemonsData: [],
      loading: false
    }
  },
  methods: {
    loadPokeList(url){
      this.loading = true
      axios.get(url)
          .then( response => {            
              const { data:{results, next, previous} } = response            
              this.next = next
              this.previous = previous
              this.getEach(results)
          })
          .catch( err => console.log(err)) 
    },

    async getEach(listOfLinks) {
      const _data = await Promise.all(listOfLinks
        .map( pokemon => {
            let pokemonInfo = axios.get(pokemon.url).then(res => res.data)
            return pokemonInfo
        }))
        this.pokemonsData = _data
        this.loading = false          
    },
    
    nextPage() {
      this.pokemonsData = []
      this.loadPokeList(this.next)
    },

    prevPage() {
      if(this.previous){
        this.pokemonsData = []
        this.loadPokeList(this.previous)
      }
    }
  },

  created () {
    this.loadPokeList(this.apiUrl) 
  },
  
}
</script>

<style>
  * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }
  html, body, #app{
    height: 100vh;
    width: 100vw;
    font-family: var(--font-text);
  }

  :root{
    --font-text: 'Quicksand', sans-serif;
    --font-heading: 'Righteous', cursive;
    --col-red: #7e0606;
    --col-red-dark: #640000;
    --col-red-darker: #4d0606;
    --col-gray-lighter: #e2dfe8;
    --col-gray-light: #a2a1a3;
    --col-gray: #4e4958;
    --col-gray-dark: #38343f;
    --col-gray-darker: #29272c;
    --col-white: #f3f3f3;
    --col-white-transparent: #f3f3f338;
    --col-vue: #42b983;
  }
  .constrict {
    width: 100%;
    max-width: 875px;
    margin-left: auto;
    margin-right: auto;
  }

  #app{
    display: flex;
    flex-direction: column;
    gap: 20px;
  }

  .pokedex {
    font-family: var(--font-heading);
    text-align: center;
    padding-top: 20px;
    color: var(--col-gray-dark)
  }

  .bttns {
    display: flex;
    height: 7vh;
    justify-content: space-evenly;
    align-items: center;
  }

  .bttns button{
    background: none;
    border: 2px solid var(--col-gray-light);
    color: var(--col-gray-light);
    width: 30%;
    height: 100%;
max-height: 84px;
font-size: 1.4rem;
  }

  .bttns button:active{
    background-color: var(--col-gray-light);
    color: var(--col-white);
  }

  footer {
    background-color: var(--col-vue);
    padding: 18px 0;
    text-align: center;
    color: var(--col-gray-dark);
    margin-bottom: 0;
    margin-top: auto;
  }
  footer a {
    text-decoration: none;
    color: var(--col-white)
  }
  footer a:hover { text-decoration: underline;}

  .normal     { background-color: #A8A77A;}
  .ground     { background-color: #E2BF65;}
  .rock       { background-color: #B6A136;}
  .bug        { background-color: #A6B91A;}
  .ghost      { background-color: #735797;}
  .steel      { background-color: #B7B7CE;}
  .fire       { background-color: #EE8130;}
  .water      { background-color: #6390F0;}
  .grass      { background-color: #7AC74C;}
  .electric   { background-color: #F7D02C;}
  .psychic    { background-color: #F95587;}
  .ice        { background-color: #96D9D6;}
  .fairy      { background-color: #D685AD;}
  .flying     { background-color: #A98FF3;color: white;}
  .fighting   { background-color: #C22E28;color: white;}
  .poison     { background-color: #A33EA1;color: white;}
  .dark       { background-color: #705746;color: white;}
  .dragon     { background-color: #6F35FC;color: white;}
</style>
