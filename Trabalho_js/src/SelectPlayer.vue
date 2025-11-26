<template>
    
  <div class="container">
      <div>
        <h1 class="titulo"> SELECT PLAYER</h1>
        <div v-if="ativo">
            <input  v-model="player" class="input-nome" type="text" placeholder="Player Name"/>
            <button class="btn" @click="salvaplayer">Next</button>
        </div>        
        <div v-else>
            <button class="btn btn-start" @click="startGame">Start Game</button> 
        </div>
           <div>
            <ul>
                <li v-for="(jogador, index) in jogadores" :key="index + jogador.nome">
                   <p> Player  {{ index + 1 }}  {{ jogador.nome }}</p> 
                </li>
            </ul>
           </div>
        </div>
            
              
    </div>
</template>
<script>


export default {
   data() {
       return {
        player: "",
        jogadores: [],
        ativo: true
           
       }
   },
   methods: {
    salvaplayer() {
        const player = {
            nome: this.player,
            partidas: 0,
            vitorias: 0,
            derrotas: 0,
            empates: 0,
            cartas:null,

        } 
        if(this.jogadores.length >=1) {
            this.ativo = false;     
        }

        this.jogadores.push(player);   
        this.player = "";
        localStorage.setItem('players', JSON.stringify(this.jogadores));
    },
    startGame() {
        this.$emit('update:Select-game', 'ArenaGame');
    },
    created(){
        if(this.jogadores.length ==""){
            return;
        }
        this.jogadores = JSON.parse(localStorage.getItem('players')) || [];
         if(this.jogadores.length >= 1) {
            this.ativo = false;
            
        }
    }
 
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
}
.btn{
    display: block;
    width: 300px;
    padding: 10px;
    font-size: 1.6rem;
    margin-bottom: 16px;
    text-transform: uppercase;
    font-weight: 600;
    background: rgb(255, 0, 0);
    border: none;
    cursor: pointer;
    color: rgb(0, 0, 0);
    font-family: fantasy;
    border: 2px solid rgb(255, 0, 0);
    border-radius: 15px;
}
.btn:hover {
    transform: scale(1.05);
    background: rgb(200, 0, 0);
}
.btn-start{
animation:  animacao 1s alternate-reverse infinite;
}
@keyframes animacao {
    from{
        transform: scale(1);
    }
    to{
        transform: scale(1.1);
    }
}

.input-nome {
    display: block;
    width: 300px;
    padding: 10px;
    margin-bottom: 16px;
    text-transform: uppercase;
    border: none;
    cursor: pointer;
    outline: none;
    font-size: 1.2rem;
    box-shadow: 0 0 5px rgba(0, 0, 0, 0.5);
}
.titulo {
    color: rgb(0, 0, 0);
   font-family: fantasy;
    font-size: 3.5rem;
    margin-bottom: 20px;
}

</style>