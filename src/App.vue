<template>
  <div id="app">
    <div v-for="(pokemon,index) in pokemons" :key="index">
      <Pokemon :name="pokemon.name" :url="pokemon" :num="index+1"/>
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
      pokemons: []
    }
  },
  created: function() {
    axios.get("https://pokeapi.co/api/v2/pokemon?offset=151&limit=151").then(res => {
      this.pokemons = res.data.results
    })
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
