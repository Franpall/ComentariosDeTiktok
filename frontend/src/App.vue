<template>
  <div v-if="first">
  <HelloWorld msg="When haces tus momos con Vue.JS"/>
  <img alt="Lo Cambia Todo" src="./assets/loCambiaTodo.jpg">
  <button @click="cambiarPagina">siguiente</button>
  </div>
  <div v-if="second">
  <HelloWorld msg="But llega ozuna"/>
  <img alt="Maluma" src="./assets/maluma.jpg">
  <audio controls>
  <source src="./assets/cancionMeme.mp3" type="audio/mpeg">
  Tu navegador no soporta la reproducción de audio.
  </audio>
  <button @click="cambiarPagina">Anterior</button>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  data(){
    return{
      first:true,
      second:false,
    };
  },
  methods: {
    cambiarPagina(){
      if (this.first){
        this.first = false;
        this.second = true;
      }
      else{
        this.first = true;
        this.second = false;
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
  color: #2c3e50;
  margin-top: 60px;
}

img{
  max-width: 96%;
}
</style>
