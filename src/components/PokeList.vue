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
    </section>
</template>

<script>
import PokeItem from './PokeItem.vue'

export default {
    name: "Pokelist",
    components: {
        PokeItem
    },
    props: ["pokemonsData"]   
}
</script>

<style scoped>

</style>