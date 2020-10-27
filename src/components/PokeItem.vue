<template>
    <a class='pokemon' @click="showDetails">
        <p>{{pokemon.name}}</p>
        <img v-bind:src="pokemon.sprites.front_default" />
    </a>

    <div class='details' v-if='detailsOpen'>
        <h1>{{pokemon.name}}</h1>
        <img v-bind:src="pokemon.sprites.front_default" />
        <a @click="hideDetails"> x </a>
    </div>

</template>

<script>
export default {
    name: 'PokeItem',
    props: ['pokemon'],
    data() {
        return { 
            detailsOpen: false
        }
    },
    methods: {
        showDetails(){
            this.detailsOpen = true
        },
        hideDetails(){
            this.detailsOpen = false
        }
    }
}
</script>

<style scoped>
.details {
    background-color: red;
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
}

.pokemon {
    padding: 8px;
    display: flex;
    flex-direction: column;
	background-color: antiquewhite;
	justify-content: space-evenly;
    transition-delay: height 3s;
}



.pokemon p {
    text-transform: capitalize;
    text-align: left;
}
.pokemon img {
    flex: 1;
    object-fit: contain;
}
</style>