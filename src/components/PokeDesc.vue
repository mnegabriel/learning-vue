<template>
    <!-- <img v-bind:src="pokeChosen.sprites.back_default || null" alt="">
    <h1>{{pokeChosen.name || null}}</h1>
    <button @click="$emit('deselect')"></button> -->

    <div class='details' v-if='detailsOpen'>
        <h1>{{pokeChosen.name}}</h1>
        <img v-bind:src="pokeChosen.sprites.front_default" />
        <a @click="hideDetails"> x </a>
    </div>
</template>

<script>
export default {
    name: 'PokeDesc',
    props: ['pokeChosen']    
}
</script>

<style scoped>

</style>