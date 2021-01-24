<template>
  <h1>Rock paper Scissors</h1>
  <p class="info">
    <span v-if="!isPlaying">You will engage in a best of 5 rounds against the browser. The side with the most points after the 5 rounds will win</span>
    <span v-if="gameOver">{{comment}}</span>
  </p>
  <button @click="togglePlay" :disabled="isPlaying" class="play">Play</button>
  <Playground v-if="isPlaying" @endGame="endGame" :gameOver="gameOver"/>
</template>

<script>
import Playground from './components/Playground.vue'

export default {
  name: 'App',
  components: {
    Playground
  },
  data(){
    return{
      isPlaying: false,
      gameOver: true,
      comment: '',
    }
  },
  methods: {
    togglePlay(){
      this.isPlaying=!this.isPlaying;
    },
    endGame(){
      this.togglePlay();
      document.querySelector('button').innerHTML='Play again!';
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
}
.info{
  margin: auto;
  max-width: 500px;
}
button{
  margin: 1em auto;
  padding: 1em 2em;
  border: 0;
  outline: none;
}
</style>
