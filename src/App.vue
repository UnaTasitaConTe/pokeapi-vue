<template>
  <div class="container mx-auto row">

    <form @submit.prevent="capturaForm()">
      <div class="input-group mt-2 mb-3">
        <input type="text" class="form-control rounded-0 border-dark" v-model="nombre_pokemon"
          placeholder="ingrese el nombre del pokemon o un número" aria-label="Recipient's username"
          aria-describedby="basic-addon2">
        <div class="input-group-append">
          <button class="btn btn-primary rounded-0 border-dark" type="submit">buscar</button>
        </div>
      </div>
    </form>

    <div class="col-4 card border-body mt-2 animate__animated animate__flash rounded-0"
      style="background-color: bisque;" v-for="pokemon in arraypokemons">
      <h1 class="text-center"> ID: {{ pokemon.id }} - NOMBRE: {{ pokemon.name.toUpperCase() }}</h1>
      <img class="img-fluid mx-auto d-block" :src="pokemon.img" :alt="pokemon.name"
        style="width: 200px; height: 200px;">
    </div>

  </div>

</template>

<script>
import axios from "axios";
import { ref } from "vue";
import PokemonInfo from './components/PokemonInfo.vue'

export default {
  components: { PokemonInfo },
  data() {
    return {
      arraypokemons: ref([]),
      nombre_pokemon: '',
      dato: ''
    }
  },
  methods: {
    capturaForm() {
      if (this.nombre_pokemon != "") {
        this.buscarPokemon(this.nombre_pokemon)
      }
    },
    buscarPokemon(name) {
      axios.get(`https://pokeapi.co/api/v2/pokemon/${name.toLowerCase()}`)
        .then((response) => {
          let pokemon = {
            id: response.data.id,
            name: response.data.name,
            img: response.data.sprites.front_default
          }
          this.dato = this.arraypokemons.find((elemento) => elemento.name === pokemon.name)

          if (this.dato === undefined) {
            this.arraypokemons.push(pokemon)
          } else {
            alert("Pokemon ya registrado o no existe")
          }
        })
        .catch(err => {
          alert("Pokemon no existe")
        })
    },
  }
};
</script>

<style>

</style>