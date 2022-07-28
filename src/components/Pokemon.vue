<template>
    <div id="pokemon">
        <div class="card">
        <div class="card-image">
            <figure>
            <img :src="current_image" alt="Placeholder image">
            </figure>
        </div>
        <div class="card-content">
            <div class="media">
            <div class="media-content">
                <p class="title is-4">{{num}} - {{ upper(name) }}</p>
                <p class="subtitle is-6">{{ pokemon.type }}</p>
            </div>
            </div>
            <div class="content">
                <button class="button is-medium" @click="change_sprite">Shiny version</button>
            </div>
        </div>
        </div>
    </div>

</template>
<script>
import axios from 'axios';
export default {
    created: function(){
        axios.get(this.url).then(res => {
            this.pokemon.type = res.data.types[0].type.name;
            this.pokemon.front = res.data.sprites.front_default;
            this.pokemon.shiny = res.data.sprites.front_shiny;
            this.current_image = this.pokemon.front;
            console.log(res)   
        })
    },
    data(){
        return{
            is_front: true,
            current_image: '',
            pokemon: {}
        }
    },
    props: {
        num: Number,
        name: String,
        url: String
    },
    methods:{
      upper: function(value){
          var newName = value[0].toUpperCase() + value.slice(1);
          return newName;
      },
      change_sprite: function(){
        if(this.is_front){
            this.is_front = false;
            this.current_image = this.pokemon.shiny;
        }else{
              this.is_front = true;
            this.current_image = this.pokemon.front;
        }
      }
  }
}




</script>
<style>
    #pokemon{
        margin-top:5%;
        width:50vh;
    }


</style>