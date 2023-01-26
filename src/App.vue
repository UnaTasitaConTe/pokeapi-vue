<template>
  <div class="container mx-auto row">
    <div class="col-4 card border-body mt-2  rounded-0" style="background-color: bisque;" v-for="pokemon in pokemons">
      <h1 class="text-center">{{ pokemon.name.toUpperCase() }}</h1>
      <img class="img-fluid mx-auto d-block" :src="pokemon.img" :alt="pokemon.name"
        style="width: 200px; height: 200px;">
      <!--  -->
      <!--componente con envio de datos-->
      <!-- <PokemonInfo :pokemon_info="pokemonSelect"></PokemonInfo> -->
      <!-- <div class="container mx-auto mt-5 text-center"> -->
      <!-- </div> -->
      <!--  -->
    </div>
    <!-- evento click sirve para más tarde -->
    <!-- <button type="button" @click="envioData()">envio</button> -->
  </div>

</template>

<script>
import axios from "axios";
import PokemonInfo from './components/PokemonInfo.vue'
export default {

  components: { PokemonInfo },
  data() {
    return {
      result: null,
      pokemons: [],
      pokemonSelect: []
    }
  },
  created() {
    for (let i = 1; i <= 21; i++) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${i}`)
        .then((response) => {
          let pokemon = {
            name: response.data.name,
            img: response.data.sprites.other.dream_world.front_default
          }
          this.pokemons.push(pokemon)
        }).catch(err => {
          console.error(err);
        })
    }
  },
  methods: {
    // creación de metodos en vue js
    // envioData(pokemon_info) {
    //   this.pokemonSelect = ["hola"]
    // }
  }
};
</script>

<style>

</style>