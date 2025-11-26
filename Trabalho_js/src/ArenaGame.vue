<template>
 <div class="container" >
  <div >
   <h1 class="titulo">{{ jogadores[turno].nome}}</h1>
   <h2>Pedra Papel Tesoura Lagarto Spock ?</h2>
   <div class="btn-icones">
    <button @click="pegarValor" value="pedra" class="btn itens"> ✊ </button>
    <button @click="pegarValor" value="papel" class="btn itens"> ✋ </button>
    <button @click="pegarValor" value="tesoura" class="btn itens"> ✌️ </button>
    <button @click="pegarValor" value="lagarto" class="btn itens"> 🤌 </button>
    <button @click="pegarValor" value="spock" class="btn itens"> 🖖 </button>
    
     </div>
  </div>
 </div>
  
</template>
<script>


export default {

  data() {
    return {
      jogadores: [],
      turno: 0
    }
  },
  methods: {
    pegarValor(event){
      this.jogadores[this.turno].cartas = event.currentTarget.value;
      localStorage.setItem('players', JSON.stringify(this.jogadores));
      this.turno++;
      if(this.turno >= this.jogadores.length){
        this.result();
      }
      
  },
  result() {
    this.$emit('update:Select-game', 'ResulatadoGame');
  }
  },
  

    created() {
      this.jogadores = JSON.parse(localStorage.getItem('players')) || [];
    }
}




</script>

<style scoped>
.container {
    width: 50%;
    height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 24px;
    color: rgb(0, 0, 0);   
}

.btn-icones{
    display: flex;
    gap: 20px;
}
.btn.itens{
    font-size: 4rem;
    background: transparent;
    border: none;
    cursor: pointer;
    }

  .btn.itens:hover { 
      animation: animaritens 0.6s  alternate infinite;
  }

  @keyframes animaritens {
    from{
        transform: translate3d(0,5px,0);
    }
    to{
         transform: translate3d(0,-5px,0);
    }
}
.titulo{
    font-size: 2rem;
    margin-bottom: 20px;
    font-family: fantasy;
}
      
</style>