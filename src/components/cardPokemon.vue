<script>
import axios from 'axios'

export default {

  created(){
    axios.get(this.url).then(res => {
      this.pokemon.type = res.data.types[0].type.name;
      this.pokemon.front = res.data.sprites.front_default;
      this.pokemon.back = res.data.sprites.back_default;
      this.currentImg = this.pokemon.front;

      console.log(this.pokemon)
      
    })
  },
  data(){
    return{
      isFront: true,
      currentImg: '', 
      pokemon: { 
        type: '',
        front: '',
        back: '',
      }
    }
  },
  props:{
    num: Number,
    name:String,
    url: String,
  },
  computed:{
    formatName(){
      const oneLetter = this.name[0].toUpperCase();
      const word =  this.name.substring(1);
      return oneLetter + word
    }
  },
  methods:{
    mudarSprite(){
      console.log('Virou')
      if(this.isFront){
        this.isFront = false;
        this.currentImg = this.pokemon.back;
        console.log('Frente')
      }else{
        this.isFront = true;
        this.currentImg = this.pokemon.front;
        console.log('costa')

      }
    }
  }

}
</script>

<template>
  <div id="pokemon">
    <div class="column is-half is-offset-one-quarter">
      <div class="card">
  <div class="card-image">
    <figure >
      <img :src='currentImg' alt="Placeholder image">
    </figure>
  </div>
  <div class="card-content">
    <div class="media">
      <div class="media-left">
       
      </div>
      <div class="media-content">
        <p class="title is-5">{{ num + 1}} - {{ formatName }}</p>
        <p class="subtitle is-6">{{ pokemon.type }}</p>
      </div>
    </div>
    <button 
    class="button is-dark is-small is-fullwidth"
    @click="mudarSprite"
    >Virar</button>

    
    
  </div>
</div>

      <!-- <h1>{{ num }}-{{ formatName }}</h1>
        <small>{{ url }}</small>
        <a :href='url' target="_blank" rel="noopener noreferrer">a</a>
      -->
      
      
    </div>
  </div>
</template>

<style scoped>
  #pokemon{
    margin-top: 2%;
  }
</style>