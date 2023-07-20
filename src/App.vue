
<script>
import axios from 'axios';
import cardPokemon from './components/cardPokemon.vue'

export default {
  name: 'App',

  components: {
    cardPokemon
  },
  created:function(){
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0').then(res=>{
      this.pokemons = res.data.results;
      this.filterPokemons = res.data.results;
      // console.log( this.pokemons);
    }).catch(error =>{
      console.log(error)

    }).finally({

    })
  },
  data(){
    return{
      pokemons: [],
      filterPokemons:[],
      busca:'',
    }
  },
  methods:{
    buscar(){
      console.log(this.pokemons)
      const stringBuscar = this.busca.toLowerCase();
      this.filterPokemons = this.pokemons;
      if(this.stringBuscar == ''|| this.stringBuscar == ' '){
       console.log('0')
        this.filterPokemons = this.pokemons;
      }else{
       console.log('1')

        this.filterPokemons = this.pokemons.filter(pokemon => pokemon.name == stringBuscar);
      }
    },
  }
  

 
}
</script>

<template>
  <div>
    
    <div class="column is-half is-offset-one-quarter">
      <img src="./assets/logo.png" alt="" srcset="">
      <h1 class="is-size-5">Pokédex com vue.js</h1>
      <input class="input is-hovered" type="text" placeholder="Buscar Pokemon" v-model="busca">
      <button 
      @click="buscar"
      class="button is-dark is-fullwidth" id="busca-btn">Buscar</button>
    </div>

    <div v-for="(pokemon,index) in filterPokemons" :key="pokemon.url">
      <cardPokemon :name="pokemon.name" :url="pokemon.url" :num="index" />
    </div>

  </div>
</template>


<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
#busca-btn{
  margin-top: 2%;
}
</style>
