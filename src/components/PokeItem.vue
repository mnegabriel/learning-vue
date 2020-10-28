<template>
    <transition name='pokemon-show' >
        <a class='pokemon' @click="showDetails">
            <p>{{pokemon.name}}</p>
            <img v-bind:src="pokemon.sprites.front_default" />
        </a>
    </transition>

    <PokeDesc 
        v-if='detailsOpen' 
        v-bind:pokeChosen="pokemon"
        v-bind:hideDetails="hideDetails"
    />
</template>

<script>
import PokeDesc from './PokeDesc'

export default {
    name: 'PokeItem',
    props: ['pokemon'],
    components: { PokeDesc },
    data() {
        return { 
            detailsOpen: false
        }
    },
    methods: {
        showDetails(){ this.detailsOpen = true },
        hideDetails(){ this.detailsOpen = false }
    }
}
</script>

<style scoped>

.pokemon {
    width: 100%;
    height: 100%;
    padding: 8px;
    display: flex;
    flex-direction: column;
	background-color: antiquewhite;
	justify-content: space-evenly;
    transition-delay: height 3s;
    position: relative;
}

.pokemon p {
    text-transform: capitalize;
    text-align: left;
    flex: 1;
}

.pokemon img {
    clip-path: inset(0 13px 13px 0px);
    width: 8rem;
    position: absolute;
    bottom: -13px;
    right: -13px;
}

</style>