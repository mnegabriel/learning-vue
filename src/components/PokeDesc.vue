<template>
    <img v-bind:src="pokeChosen.sprites.back_default || null" alt="">
    <h1>{{pokeChosen.name || null}}</h1>
    <button @click="$emit('deselect')"></button>
</template>

<script>
export default {
    name: 'PokeDesc',
    props: ['pokeChosen']    
}
</script>

<style scoped>

</style>