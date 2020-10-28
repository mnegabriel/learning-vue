<template>
    <div class='details'>
        <div class='constrict'>

            <div class='identity'>
                <h1>{{pokeChosen.name}}</h1>
                <p> 
                    Index: 
                    {{grabIndex(pokeChosen)}}
                </p>

                <h2>Base Stats</h2>

                <div class='base-stats'>
                    <div 
                    class='base-stat'
                    v-for="stat in pokeStats" 
                    v-bind:key="pokeStats[stat]"
                    >
                        <h5>{{stat.stat.name}}</h5>
                        <p>{{stat.base_stat}}</p>
                    </div>
                    

                </div>
            </div>

            <div class='avatar'>
                <img v-bind:src="pokeChosen.sprites.front_default" />
            </div>


            <div class='sprites' >
                
                <img  
                v-bind:src="image" 
                v-for="image in existingImages" 
                v-bind:key="existingImages[image]"
                />
            </div>

            <div @click="hideDetails" class='btn-close'>
                <p> Close </p>
            </div>
        </div>
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
        },
        pokeStats: function() {
            return this.pokeChosen.stats
        }
    }
}
</script>

<style scoped>
.details {
    z-index: 100;
    background: repeating-linear-gradient(to bottom, rgba(51, 47, 61, 0.959),rgba(51, 47, 61, 0.925) 5px);
    height: 100vh;
    width: 100vw;
    position: fixed;
    top: 0;
    left: 0;
    display: grid;
}

.details .constrict{
    border-top: 10px solid white;
    padding: 30px;
    background-color: rgb(143, 25, 44);
    display: grid;
    grid-template-areas:
        'NAME AVAT AVAT'
        'PICS PICS PICS'
        'CLOS CLOS CLOS'
    ;
}

.identity { 
    grid-area: NAME; 
    border-top: 3px solid white;
    display: flex;
    flex-direction: column;
    gap: 10px;
    position: relative;

    color: white;
}

.identity h1{
    font-family: var(--font-heading);
    text-transform: uppercase;
    background-color: white;
    color: #630000;
}
.identity > p{
    position: absolute;
    right: 0;
    top: 30px;
    background-color: rgba(255, 255, 240, 0.24) ;
    padding: 4px 8px;
    font-weight: bold;
}

.base-stats{
    background-color: #630000af;
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 8px;

}

.base-stat{
    display: flex;
    align-items: flex-end;
}
.base-stat h5 {
    border-bottom: 1px solid white;
    flex: 1;
}
.base-stat p {
    background-color: white;
    color: #630000;
    width: 45px;
    text-align: center;
    font-family: var(--font-heading);
}

.avatar { 
    border-top: 3px solid white;
    grid-area: AVAT; 
    width: 100%;
    display: flex;
    justify-content: flex-end;
    align-items: baseline;
}

.avatar img{
    max-width: 12rem;
    flex: 1;
}

.sprites { 
    grid-area: PICS; 
    display:flex;
    width: 100%;
    align-items: center;
    justify-content: space-evenly;
    flex-wrap: wrap;
    padding: 0 10px;
    background-color: rgb(78, 0, 0);
    margin-bottom: 30px;
    position: relative;
}
.sprites::before {
    content: 'Sprites';
    position: absolute;
    top: -15px;
    left: 0;
    font-size: 1.6rem;
    color: rgb(78, 0, 0);
    width: 100%;
    font-weight: bold;
    text-transform: uppercase;
    background-color: white;
} 

.btn-close { 
    grid-area: CLOS;
    width:100%;
    height: 50%;
    border-top: 3px solid white;
    background-color: rgba(255, 255, 240, 0.24);
    color: rgb(143, 25, 44);
    display:flex;
    justify-content: center;
    align-items: center;
    font-size: 4rem;
    font-family: var(--font-heading);
}


</style>