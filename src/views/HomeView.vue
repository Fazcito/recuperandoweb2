<template>
  <div class="home">
    <div class="header">

    </div>

    <div class="main">
      <div class="pokeimagenes">
        <div v-for="imagen in imagenes" :key="imagen.id">
          <img :src="imagen.imagen" alt="">
          <p>{{ imagen.nombre }}</p>
          <p :style="{ backgroundColor: imagen.type_color }">{{imagen.type_name}}</p>
          
        </div>
      </div>
    </div>


  </div>
</template>

<script>

import axios from 'axios';
export default {
  name: 'HomeView',

  data() {
    return {
      imagenes: [],
      nombre: [],
    }
  },

  methods: {
    getImagenes: async function () {
      const urlImagenes = 'https://cobuses.com.co/APIV2/model/pokemon.php?dato=getallpokemon'
      const vue = this;

      await axios
        .get(urlImagenes)
        .then(function (response) {

          vue.imagenes = response.data;
          console.log(response.data);
        })
        .catch(function (error) {
          console.log(error);
        })
        .finally(function () {
          console.log("La petición finalizó");
        })


    }
  },
  created: function(){
  this.getImagenes();
}

}


</script>

<style scoped>
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;

}

.pokeimagenes {
  display: grid;
  grid-template-columns: repeat(6, 1fr);
  grid-auto-rows: repeat(5, 1fr);
}

.img{
  height: 12rem;
  object-fit: cover;
}
</style>
