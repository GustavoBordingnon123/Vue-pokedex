<template>
  
    <div class="column is-full is-offset-half">
      <h2 class="is-size-1">Pokedex</h2>
      <input type="text" placeholder="Buscar pokemon pelo nome em minusculo" v-model="busca" class="input is-normal">
      <button id="button" class="button is-primary is-fullwidth" @click="buscar">Buscar</button>
      <div v-for="(poke,index) in filtered_pokemons" :key="poke.url">
        <Pokemon :name="poke.name" :url="poke.url" :num="index+1"/>
      </div>
    </div>

</template>

<script>
import axios from 'axios';
import Pokemon from './components/Pokemon.vue'

export default {
  name:'App',
  data(){
    return {
      pokemons: [],
      filtered_pokemons: [],
      busca: ''
    }
  },
  created: function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res =>{
      console.log('catch pokemons list');
      this.pokemons = res.data.results;
      this.filtered_pokemons = res.data.results;
    })
  },
  components: {
    Pokemon
  },methods: {
    buscar: function(){
      this.filtered_pokemons = this.pokemons;
      if(this.busca == '' || this.busca == ' '){
        this.filtered_pokemons = this.pokemons;
      }else{
        this.filtered_pokemons = this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
  },
  computed: {

/*
    resultado_busca: function(){
      if(this.busca == '' || this.busca == ' '){
        return this.pokemons;
      }else{
        return this.pokemons.filter(pokemon => pokemon.name == this.busca);
      }
    }
*/
  }
}
    

</script>

<style>
  #app{
    font-family: Avenir,Arial, Helvetica, sans-serif;
    -webkit-font-smoothing:antialiased;
    -moz-osx-font-smoothing:grayscale;
    text-align: center;
    margin-top:60px;
  }

  #button {
    margin-top:3%;
  }
</style>