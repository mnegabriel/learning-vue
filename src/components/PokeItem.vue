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
    />
    <!-- <div class='details' v-if='detailsOpen'>
        <h1>{{pokemon.name}}</h1>
        <img v-bind:src="pokemon.sprites.front_default" />
        <a @click="hideDetails"> x </a>
    </div> -->

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
.details {
    background-color: rgb(255, 224, 224);
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
}

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