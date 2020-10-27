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
  }
</style>
