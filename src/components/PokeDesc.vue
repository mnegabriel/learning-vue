<template>
    <div class='details'>
        <div class='constrict'>

            <div class='identity'>
                <h1>{{pokeChosen.name}}</h1>

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
                <p> 
                    Index: 
                    {{grabIndex(pokeChosen)}}
                </p>
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
    border-top: 10px solid var(--col-white);
    padding: 30px;
    background-color: var(--col-red);
    display: grid;
    grid-template-areas:
        'NAME AVAT AVAT'
        'PICS PICS PICS'
        'CLOS CLOS CLOS'
    ;
}

.identity { 
    grid-area: NAME; 
    border-top: 3px solid var(--col-white);
    display: flex;
    flex-direction: column;
    gap: 50px;
    position: relative;

    color: var(--col-white);
    font-size: .8rem;
}

.identity h1{
    font-family: var(--font-heading);
    text-transform: uppercase;
    background-color: var(--col-white);
    color:var(--col-red);
}

.base-stats{
    grid-area:STAT;
    background-color: var(--col-red-dark);
    padding: 20px;
    display: flex;
    flex-direction: column;
    gap: 8px;
    position:relative;

}
.base-stats::before {
    content: 'Base Stats';
    position: absolute;
    top: -24px;
    left: 0;
    font-size: 1.2rem;
    color: var(--col-red);
    padding: 0 5px;
    font-weight: bold;
    text-transform: uppercase;
    background-color: var(--col-white);
} 

.base-stat{
    display: flex;
    align-items: flex-end;
}
.base-stat h5 {
    border-bottom: 1px solid var(--col-white);
    flex: 1;
}
.base-stat p {
    background-color: var(--col-white);
    color: #630000;
    width: 45px;
    text-align: center;
    font-family: var(--font-heading);
}

.avatar { 
    border-top: 3px solid var(--col-white);
    grid-area: AVAT; 
    width: 100%;
    display: flex;
    justify-content: flex-end;
    align-items: baseline;
    position: relative;
}
.avatar > p{
    position: absolute;
    right: 0;
    background-color: var(--col-white-transparent) ;
    padding: 4px 8px;
    font-weight: bold;
    color: var(--col-white);
}

.avatar img{
    align-self: normal;
    flex: 1;
    max-width: 14rem;
    max-height: 14rem;
}

.sprites { 
    grid-area: PICS; 
    display:flex;
    width: 100%;
    align-items: center;
    justify-content: space-evenly;
    flex-wrap: wrap;
    padding: 0 40px;
    background-color: var(--col-red-darker);
    margin-bottom: 30px;
    position: relative;
}
.sprites::before {
    content: 'Sprites';
    position: absolute;
    top: -30px;
    left: 0;
    font-size: 1.6rem;
    color: var(--col-red);
    width: 100%;
    font-weight: bold;
    text-transform: uppercase;
    background-color: var(--col-white);
} 

.btn-close { 
    grid-area: CLOS;
    width:100%;
    height: 50%;
    border-top: 3px solid var(--col-white);
    background-color: var(--col-white-transparent);
    color: var(--col-red-dark);
    display:flex;
    justify-content: center;
    align-items: center;
    font-size: 4rem;
    font-family: var(--font-heading);
    border-bottom: 3px solid var(--col-red-dark)
}

@media(max-width:400px){
    .details .constrict {
        padding: 0;
    }
}
@media(max-width:780px){
    .sprites {
        margin: 0;
    }
}


</style>