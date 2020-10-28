<template>
    <div class='details'>
        <h1>{{pokeChosen.name}}</h1>
        <p> 
            Index: 
            {{grabIndex(pokeChosen)}}
        </p>
        <img v-bind:src="pokeChosen.sprites.front_default" />

        <div class='sprites' >
            <img  
            v-bind:src="image" 
            v-for="image in existingImages" 
            v-bind:key="existingImages[image]"
            />
        </div>
        <a @click="hideDetails"> Close </a>
    </div>
</template>

<script>

export default {
    name: 'PokeDesc',
    props: [ 'pokeChosen', 'hideDetails' , 'grabIndex'],
    data() {
        return { images: Object.values(this.pokeChosen.sprites) }
    },
    computed: {
        existingImages: function() {
            return this.images.filter( image => {
                return typeof image === 'string' || image instanceof String
            })
        }
    }
}
</script>

<style scoped>
.details {
    z-index: 100;
    background-color: rgb(230, 38, 255);
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
    display: grid;
}

.details h1 {
    text-transform: uppercase;
}

.details > img {
    width: 12rem;
}

.sprites {
    display:flex;
    width: 100%;
    align-items: center;
    justify-content: space-evenly;
    flex-wrap: wrap;
    padding: 0 10px;
}

.sprites img {
    margin: 0 -10px;
    /* width: 5rem; */
}

</style>