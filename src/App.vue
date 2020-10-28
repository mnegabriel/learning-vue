<template>
  <h1>List of pokemons:</h1>
  <PokeList 
    v-bind:pokemonsData='pokemonsData' 
    v-bind:loading="loading"
  />
  <button type="button" @click="prevPage"> ⏪ </button>
  <button type="button" @click="nextPage"> ⏩ </button>
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
  }
  .constrict {
    width: 100%;
    max-width: 875px;
    margin-left: auto;
    margin-right: auto;
  }

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
