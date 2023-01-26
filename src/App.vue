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
      <h5 class="text-center"> ID: {{ pokemon.id }} - NOMBRE: {{ pokemon.name.toUpperCase() }}</h5>
      <img class="img-fluid mx-auto d-block" :src="pokemon.img" :alt="pokemon.name"
        style="width: 200px; height: 200px;">
    </div>

    <PokemonInfo>
      <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Numquam accusamus porro minus fugiat minima quos ipsa
        enim repellendus fuga aut! Rerum autem officia odit, placeat cum dolores ullam dolor rem?</p>
    </PokemonInfo>


    <footer></footer>

  </div>
</template>

<script>
import axios from "axios";
import { ref } from "vue";
import PokemonInfo from './components/PokemonInfo.vue'
import Footer from "./components/Footer.vue";

export default {
  components: { PokemonInfo, Footer },
  data() {
    return {
      arraypokemons: ref([]),
      nombre_pokemon: '',
      dato: ''
    }
  },
  created() {
    if (localStorage.getItem('pokemons') != null) {
      this.arraypokemons = JSON.parse(localStorage.getItem('pokemons'))
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
          this.dato === undefined ? (this.arraypokemons.push(pokemon))
            : (alert("Pokemon ya registrado o no existe"))
          localStorage.setItem('pokemons', JSON.stringify(this.arraypokemons));

        }).catch(err => {
          console.log(err);
          alert("Error al conectarse o al buscar al pokemon")
        })
    },

  }
};
</script>
<style>

</style>