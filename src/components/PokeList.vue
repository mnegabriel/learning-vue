<template>
    <section class='pokemonList'>

        <ul class='constrict'>
            <transition-group 
            name='list' 
            enter-active-class="animate__animated animate__fadeIn" 
            >
                <li
                v-for="pokemon in pokemonsData"
                v-bind:key='pokemon.id'
                >
                    <PokeItem v-bind:pokemon="pokemon" />
                </li>
            </transition-group>
        </ul>

        <transition name='pokemon-show' >
            <div id='loading' v-if="loading" >
                <h2> L o a d i n g . . . </h2>  
            </div> 
        </transition>  

    </section>
</template>

<script>
import PokeItem from './PokeItem.vue'

export default {
    name: "Pokelist",
    components: { PokeItem },
    props: ["pokemonsData", 'loading'],
}
</script>

<style scoped>
ul {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    grid-template-rows: repeat(3, 1fr);
    gap: 20px;
    list-style: none;
    height: 100%;
}

section {
    padding: 30px 10px;
    position: relative;
    height: 70vh;
    background-color: var(--col-gray-lighter);
}

#loading {
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    background: rgba(226, 226, 226, 0.589);
    display: flex;
    justify-content: center;
    align-items: center;
}

.pokemon-show-enter-active {
    animation: loading-overlay .5s;
}

.pokemon-show-leave-active {
    animation: loading-overlay .5s reverse;
}

@keyframes loading-overlay {
    0% { clip-path: circle(0 at 50% -50%); }
    100% { clip-path: circle(200% at 50% -50%); }
}

.animate__animated.animate__fadeIn{
    --animate-delay: 1s;
}

@media(max-width: 480px){
    section { padding: 30px 0; }
    ul { gap: 10px; }
}
</style>