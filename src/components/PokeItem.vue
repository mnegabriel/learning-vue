<template>
        <a class='pokemon' @click="showDetails">

            <div class='pokemon__info'>

                <p class='pokemon__name'>{{pokemon.name}}</p>
                <p class='pokemon__index'>n.{{grabIndex(pokemon)}}</p>

                <div class='stats'>

                </div>

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

    <transition
    enter-active-class="animate__animated animate__fadeIn" 
    leave-active-class="animate__animated animate__fadeOut" 
    >
        <PokeDesc 
            v-if='detailsOpen' 
            v-bind:pokeChosen="pokemon"
            v-bind:hideDetails="hideDetails"
            v-bind:grabIndex="grabIndex"
        />
    </transition>

</template>

<script>
import PokeDesc from './PokeDesc'

export default {
    name: 'PokeItem',
    props: ['pokemon'],
    components: { PokeDesc },
    data() {
        return { detailsOpen: false }
    },
    methods: {
        showDetails(){ this.detailsOpen = true },
        hideDetails(){ this.detailsOpen = false },
        grabIndex(pokemon){
            return pokemon.game_indices[pokemon.game_indices.length - 1].game_index
        }
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
	background-color: var(--col-white);
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
    font-size: clamp(1rem, 2.7vw, 1.5rem);
    font-family: var(--font-heading);
    color: var(--col-gray)
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

.pokemon__index {
    background-color: #323232;
    color: #ffffff;
    padding: 3px 8px;
    border-radius: 3px;
    position: absolute;
    top: 5px;
    right: 5px;
    font-size: .8rem;
}

.animate__animated.animate__fadeIn{
    --animate-duration: 100ms;
    --animate-delay:0;
}

.animate__animated.animate__fadeOut{
    --animate-duration: 100ms;
    --animate-delay:0;

}

@media (min-width: 700px){

    .pokemon {
        flex-direction: row;
    }
    .pokemon__info,
    .pokemon__types{
        flex-direction: column;
    }

    .pokemon__name {
        align-self: flex-start;
    }

    .pokemon__types{
        position:initial;
        gap: 5px;
    }

    .pokemon__type{
        border-radius: 4px;
    }

    .pokemon__type p {
        position:initial;
        display: block;
        text-align: center;
        text-transform: uppercase;
        padding: 3px 0;
    }

    .pokemon__index{
        right: initial;
        left: 5px;
    }
@media (min-width: 1070px){
    .pokemon__types{
        flex-direction: row;
        justify-content: flex-end;
    }
}


    /* .pokemon img {

        clip-path: inset(0 13px 13px 0px);
        width: 8rem;
        position: absolute;
        bottom: -13px;
        right: -13px;
    } */
    
}
</style>