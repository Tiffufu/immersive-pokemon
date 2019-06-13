<template>
  <div id="app">
    <div class="container">
      <h1 class="text-center display-2">Rock Type Pokemon</h1>
      <div class="row">
    <!-- Looks through the card 82 times (for each rock type Pokemon -->
    <card :url="item.pokemon.url" v-for="item in pokemonOfRockType" :key="item.pokemon.name"></card> 
</div>
</div>
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
      console.log(response.data.pokemon);
      // vm.pokemonOfRockType makes VueJS aware of this object.
      // Axios will later inject data into pokemonOfRockType object when it loads
      vm.pokemonOfRockType = response.data.pokemon
    });
  }
}
</script>