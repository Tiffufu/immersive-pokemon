<template>
  <div id="app">
    <div class="container">
      <h1 class="text-capitalize text-center display-3">{{ activeType }} Type Pokemon</h1>
      <button class="m-1 btn btn-info text-capitalize" :key="type" v-for="type in types" @click="changeType(type.name)">
        {{ type.name }}
      </button>
      <div class="mt-3 row">
    <!-- Looks through the card 82 times (for each rock type Pokemon -->
    <card :url="item.pokemon.url" v-for="item in pokemonOfCurrentType" :key="item.pokemon.name"></card> 
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
      pokemonOfCurrentType: "",
      types: "",
      activeType: "normal"
      }
    },
  methods: {
    changeType: function(name) {
      this.activeType = name;
      this.retrievePokemonOfSpecifiedType(name);
    },
    retrievePokemonOfSpecifiedType: function(type) {
      const axios = require('axios');
      const vm = this;
      axios({
          method: 'get',
          url: 'https://pokeapi.co/api/v2/type/' + type
      })
      .then(function (response) {
          // console.log(response.data.pokemon);
          vm.pokemonOfCurrentType = response.data.pokemon
      });
    }
  },
    mounted: function() {

    const axios = require('axios');
    const vm = this;

    axios({
    method: 'get',
    url: 'https://pokeapi.co/api/v2/type/' + this.activeType
    })
    .then(function (response) {
      console.log(response.data.pokemon);
      // vm.pokemonOfCurrentType makes VueJS aware of this object.
      // Axios will later inject data into pokemonOfCurrentType object when it loads
      vm.pokemonOfCurrentType = response.data.pokemon
    });

     axios({
    method: 'get',
    url: 'https://pokeapi.co/api/v2/type',
    })
    
    .then(function (response) {
      console.log(response.data.results);
      // vm.pokemonOfCurrentType makes VueJS aware of this object.
      // Axios will later inject data into pokemonOfCurrentType object when it loads
      vm.types = response.data.results
    });
  }
}
</script>