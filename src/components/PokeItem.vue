<template>
    <button @click="showDetails">
        <p>{{pokemon.name}}</p>
        <img v-bind:src="pokemon.sprites.front_default" />
    </button>

    <div class='details' v-if='detailsOpen'>
        <h1>{{pokemon.name}}</h1>
        <img v-bind:src="pokemon.sprites.front_default" />
        <button @click="hideDetails"> x </button>
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
</style>