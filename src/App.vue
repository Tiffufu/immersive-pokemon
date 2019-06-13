<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <!-- Looks through the card 82 times (for each rock type Pokemon -->
    <card :url="item.pokemon.url" v-for="item in pokemonOfRockType" :key="item.pokemon.name"></card> 

    <!-- <div v-for="item in pokemonOfRockType" :key="item.pokemon.name">
      {{ item.pokemon.name }}
    </div> -->
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import card from './components/card.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    card
  },
    data: function () {
      return {
      //Creates meaningful object for VueJs to link to
      pokemonOfRockType: ""
      }
    },
    mounted: function() {

    const axios = require('axios');
    const vm = this;

    axios({
    method: 'get',
    url: 'https://pokeapi.co/api/v2/type/rock',
    responseType: 'stream'
    })
    
    .then(function (response) {
      // console.log(response.data.pokemon);
      // vm.pokemonOfRockType makes VueJS aware of this object.
      // Axios will later inject data into pokemonOfRockType object when it loads
      vm.pokemonOfRockType = response.data.pokemon
    });
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
