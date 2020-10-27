<template>
    <section class='pokemonList'>
        <h1>List of pokemons:</h1>

        <ul>
            <li class="pokemonList__item" 
                v-bind:key='pokemon.id' 
                v-for="pokemon in pokemonsData">

                <PokeItem v-bind:pokemon="pokemon" />
            </li>
        </ul>
        <h4 v-if="loading" > L o a d i n g . . . </h4>
    </section>
</template>

<script>
import PokeItem from './PokeItem.vue'

export default {
    name: "Pokelist",
    components: {
        PokeItem
    },
    props: ["pokemonsData", 'loading'],
     
}
</script>

<style scoped>
ul {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 20px;
    list-style: none;
    padding: 30px 0;
}
</style>