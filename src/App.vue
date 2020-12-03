<template>
  <div id="app">
    <div class="column is-half is-offset-one-quarter">
      <input class="input is-rounded" type="text" v-model="busca">
      <button id="busca" class="button is-danger is-outlined is-fullwidth" @click="buscar">Buscar</button>
      <div v-for="(pokemon,index) in filteredPokemons" :key="index">
        <Pokemon :name="pokemon.name" :url="pokemon" :num="index+1"/>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon'
export default {
  name: 'App',
  components: {
    Pokemon
  },
  data() {
    return {
      pokemons: [],
      filteredPokemons: [],
      busca: ''
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?offset=151&limit=151").then(res => {
      this.pokemons = res.data.results
      this.filteredPokemons = res.data.results
    })
  },
  methods: {
    buscar: function() {
      this.filteredPokemons = this.pokemons
      if ( this.busca == '' || this.busca == ' ' ) {
        this.filteredPokemons = this.pokemons
      } else {
        this.filteredPokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca)
      }
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  background-color: #2c3e50;
}

#busca{
  margin-top: 2%;
}
</style>
