<template>
  <div class="col-3" v-if="pokemon.sprites && pokemon.sprites.front_default">
    <div class="card" style="width: 18rem;">
      <div class="card-body">
        <img :src="pokemon.sprites['front_default']" :alt="pokemon.name">
        <!-- <img class="card-img-top" v-bind:src="pokemon.sprites.front_default" v-bind:alt="pokemon.name"> -->
        <h5 class="text-capitalize card-title"> {{ pokemon.name }}</h5>
        <p class="card-text mb-0">Height: {{ (pokemon.height * 3.937).toFixed(2) }} inches</p>
        <p class="card-text mt-0">Weight: {{ (pokemon.weight / 4.536).toFixed(2) }} lbs</p>
      </div>
    </div>
  </div>
  <span class="d-none" v-else>
  </span>
</template>

<script>
  export default {
    name: 'card',
    data: function () {
      return {
        pokemon: ""
      }
    },
    props: {
      url: String
    },
    mounted: function () {

      const axios = require('axios');
      const vm = this;

      axios({
          method: 'get',
          url: vm.url,
          responseType: 'stream'
        })

        .then(function (response) {
          // console.log(response.data);
          vm.pokemon = response.data
        });
    }
  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  h3 {
    margin: 40px 0 0;
  }

  ul {
    list-style-type: none;
    padding: 0;
  }

  li {
    display: inline-block;
    margin: 0 10px;
  }

  a {
    color: #42b983;
  }
</style>