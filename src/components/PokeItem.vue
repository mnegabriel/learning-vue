<template>
    <transition name='pokemon-show' >
        <a class='pokemon' @click="showDetails">

            <div class='pokemon__info'>

                <p class='pokemon__name'>{{pokemon.name}}</p>
                <p class='pokemon__index'>n.{{pokemon.order}}</p>

                <div class="pokemon__types" >
                    <div 
                    v-for='type in pokemon.types' 
                    class="pokemon__type"
                    v-bind:class="type.type.name"
                    v-bind:key='type.type.slot'
                    >
                        <p>{{type.type.name}}</p>
                    </div>
                </div>

            </div>
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
            detailsOpen: false,
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
    position: relative;
    width: 100%;
    height: 100%;
    padding: 8px;
    display: flex;
    flex-direction: column;
	background-color: antiquewhite;
	justify-content: space-evenly;
}

.pokemon__info{
    order: 2;
    flex: 1;
    display:flex;
    align-items: center;
    justify-content: space-between;
    
}

.pokemon__name {
    text-transform: capitalize;
}

.pokemon img {
    object-fit: contain;
}

.pokemon__types{
    display:flex;
    position: absolute;
    bottom: 0;
    left: 0;
    width:100%;
}

.pokemon__type {
    min-height: 8px;
    flex: 1;
}
.pokemon__type p {
    display: none
}

@media (min-width: 700px){

    .pokemon p {
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
    
}
</style>