<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png" /> -->
  <!--<HelloWorld msg="Hello Vue 3 + Vite" /> -->
  <div class="grid-container">
    <div class="weather-main">
      <Weather />
    </div>
    <div class="quotes-main">
      <Quotes />
    </div>
    <div class="beers-main">
      <Beers />
    </div>
  </div>
</template>

<script>
// This starter template is using Vue 3 <script setup> SFCs
// Check out https://v3.vuejs.org/api/sfc-script-setup.html#sfc-script-setup
import HelloWorld from './components/HelloWorld.vue'
import Weather from './components/Weather.vue'
import Quotes from './components/Quotes.vue'
import Beers from './components/Beers.vue'


export default {
  name:'App',
  components: {
    Weather,
    Quotes,
    Beers,
  },
}
</script>



<style>
#app {
  box-sizing:border-box;
}


.weather-main {
  text-align: center;
  height:fit-content;
  background-color:black;
  padding:25px;
  /* grid-area: weather;  */ 
}
.quotes-main {
  height:fit-content;
  background-color:brown;
  padding:25px;
}
@media (max-width: 1000px) {
    .weather-main {
      display:flex;
      flex-direction:column;
    }
    .quotes-main {
      display:flex;
      flex-direction:column;
    }
    .beers-main {
      display:flex;
      flex-direction:column;
    }
    
  }



.beers-main {
  background-color: black;
  height:fit-content;
}


</style>
