
<template>
 <div id="App">

  <Transition name="fete" mode="out-in">
    <component @update:Select-game="componenteAtivo = $event" :is="componenteAtivo"></component>
  </Transition>
   

 </div>
</template>
<script >



import StartGame from './StartGame.vue';
import SelectPlayer from './SelectPlayer.vue';
import ArenaGame from './ArenaGame.vue';
import ResulatadoGame from './ResulatadoGame.vue';


export default {
  name: 'App',  
  data() {
    return {
      mensagem: 'Hello Vue!',
      componenteAtivo : 'StartGame'
    }
  }, components: {
    StartGame,
    SelectPlayer,
    ArenaGame,
    ResulatadoGame
   
  }
};

</script>


<style >

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}


html, body {
  height: 100%;
  width: 100%;


background-image: url("https://image.geekship.com.br/OrV2BiyAfqCxnAy4F7DNCXSU23w=/2240x0/smart/filters:strip_icc():format(webp)/hull.geekship.com.br/wp-content/uploads/2024/01/R-1-1.jpeg");
background-size: cover;

font-family: fantasy;
color: rgb(248, 248, 248); 
} 



input, button {
  font-family: fantasy;
}
.fete-enter-active, .fete-leave-active {
  transition: opacity 0.5s;
}
.fete-enter, .fete-leave-to /* .fade-leave-active below version 2.1.8 */ {
  opacity: 0;
}
</style>
