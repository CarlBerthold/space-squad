<template>

<div class="grid-container">
    <h1>Fancy Beers for the feierabend</h1>
<div class="card"
  v v-for="beer of beers" :key="beer">
    <div class="name">
          <h2>{{beer.name}}</h2>
    </div>
          <img v-bind:src="beer.image_url">
    
          <p>{{beer.tagline}}</p>
          <!-- <p>{{beer.description}}</p> -->
    
    
</div>
</div>
</template>

<script>
import axios from 'axios';

export default {
    data(){
        return {
            beers:[],
        }
    },
    methods: {
        getBeers(){
        axios.get("https://api.punkapi.com/v2/beers")
        .then((response)=> {
        console.log(response.data)
        this.beers=response.data
        })
        .catch((err)=> console.log(err))
        }
    },
    beforeMount(){
        this.getBeers()
    },
}
</script>

<style scoped>

h1{
    margin:auto;
    text-align: center;
    color:white;
}

.grid-container{
    padding:25px;
    display:grid;
    grid-template-columns: 1fr 1fr 1fr 1fr;
    row-gap:50px;
    column-gap:50px;

}
@media (max-width: 1000px){
    .grid-container{
        display:Grid;
        grid-template-columns: 1fr 1fr;
        
    }
}


.name{
padding:25px;

}

img {
    height: auto; 
    width: auto; 
    max-width: 300px; 
    max-height: 300px;
    align-self: center;


}

.tagline{
    background-color:green;
    /* grid-column: 3/3; */
    text-align: center;
    /* grid-area:tagline; */

}

.card{
  padding-top:10px;
  text-align: center;
   /* border: 1px solid black;  */
  /* border-top-right-radius:36%;
  border-top-left-radius:36%; */
  height: 500px;
  background-color: blanchedalmond;
  border-radius: 3px;
  
}
</style>