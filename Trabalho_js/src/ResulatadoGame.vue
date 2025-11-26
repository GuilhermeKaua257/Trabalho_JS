<template>
 
  <div class="container">
    <div class="placar">
  <h2>PLACAR</h2>

  <div class="linha">
    <strong>{{ jogadores[0].nome }}:</strong>
    <span>V: {{ jogadores[0].vitorias }}</span>
    <span>D: {{ jogadores[0].derrotas }}</span>
    <span>E: {{ jogadores[0].empates }}</span>
  </div>

  <div class="linha">
    <strong>{{ jogadores[1].nome }}:</strong>
    <span>V: {{ jogadores[1].vitorias }}</span>
    <span>D: {{ jogadores[1].derrotas }}</span>
    <span>E: {{ jogadores[1].empates }}</span>
  </div>
</div>
    <h1 class="titulo">RESULTADO</h1>

    <div class="box">

      <!-- EMPATE -->
      <p v-if="resultado === 'empate'" class="empate">Empate!</p>

      <!-- VENCEDOR -->
      <div v-else>
        <p class="texto">
          Vencedor: <strong>{{ vencedor.nome }}</strong> ({{ vencedor.cartas.toUpperCase() }})
        </p>
        <p class="texto">
          Perdedor: <strong>{{ perdedor.nome }}</strong> ({{ perdedor.cartas.toUpperCase() }})
        </p>
      </div>

      <!-- FRASE DO DUELO -->
      <p class="frase" v-if="fraseDuelo">
        {{ fraseDuelo }}
      </p>

      <button class="btn-voltar" @click="voltar">
        Jogar Novamente
      </button>

    </div>
    
  </div>
  
</template>

<script>
export default {
  data(){
    return{
      jogadores: [],
      vencedor: null,
      perdedor: null,
      resultado: "",
      fraseDuelo: "",

      regras: {
        tesoura: ["papel", "lagarto"],
        papel: ["pedra", "spock"],
        pedra: ["lagarto", "tesoura"],
        lagarto: ["spock", "papel"],
        spock: ["tesoura", "pedra"]
      },

 

      frases: {
        "tesoura-papel": "Tesoura corta papel ✂️",
        "papel-pedra": "Papel cobre pedra 📄",
        "pedra-lagarto": "Pedra esmaga lagarto 🪨",
        "lagarto-spock": "Lagarto envenena Spock 🦎",
        "spock-tesoura": "Spock esmaga tesoura 🖖",
        "tesoura-lagarto": "Tesoura decapita lagarto ✂️🦎",
        "lagarto-papel": "Lagarto come papel 🦎📄",
        "papel-spock": "Papel refuta Spock 📄🖖",
        "spock-pedra": "Spock vaporiza pedra 🖖💥",
        "pedra-tesoura": "Pedra quebra tesoura 🪨✂️"
      }
    }
  },

  created() {
    this.jogadores = JSON.parse(localStorage.getItem("players")) || [];
    this.validar();
  },

  methods: {

    validar(){
      const p1 = this.jogadores[0];
      const p2 = this.jogadores[1];

      // EMPATE
      if (p1.cartas === p2.cartas) {
        this.resultado = "empate";
        this.fraseDuelo = "Ambos escolheram a mesma jogada.";
        p1.empates++;
        p2.empates++;
        this.salvar();
        return;
      }

      // VERIFICA VENCEDOR
      if (this.regras[p1.cartas].includes(p2.cartas)) {
        this.vencedor = p1;
        this.perdedor = p2;
        p1.vitorias++;
        p2.derrotas++;
        this.definirFrase(p1.cartas, p2.cartas);
      } else {
        this.vencedor = p2;
        this.perdedor = p1;
        p2.vitorias++;
        p1.derrotas++;
        this.definirFrase(p2.cartas, p1.cartas);
      }

      this.resultado = "vencedor";
      this.salvar();
    },

    definirFrase(golpeVencedor, golpePerdedor){
      const chave = `${golpeVencedor}-${golpePerdedor}`;
      this.fraseDuelo = this.frases[chave] || "";
    },

    salvar(){
      localStorage.setItem("players", JSON.stringify(this.jogadores));
    },

    voltar(){
      this.$emit("update:Select-game", "ArenaGame");
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
    color: rgb(0, 0, 0);   
}

.titulo{
    font-size: 2rem;
    margin-bottom: 20px;
    font-family: fantasy;
}

.box {
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 16px;
}

.texto {
    font-size: 1.5rem;
    font-family: fantasy;
}

.empate{
    font-size: 2rem;
    font-family: fantasy;
    color: rgb(0, 0, 150);
}

.frase{
    font-size: 1.4rem;
    font-family: fantasy;
    margin-top: 10px;
    color: rgb(80, 0, 0);
    text-align: center;
}
/* PLACAR FIXO NO CANTO SUPERIOR ESQUERDO */
.placar {
    position: fixed;
    top: 20px;
    left: 20px;

    background: rgba(255, 0, 0, 0.7);
    padding: 12px 18px;
    border-radius: 12px;
    font-family: fantasy;
    border: 2px solid black;

    display: flex;
    flex-direction: column;
    gap: 6px;
}

.placar h2 {
    font-size: 1.3rem;
    margin: 0;
}

.placar .linha {
    display: flex;
    gap: 10px;
    font-size: 1rem;
}


.btn-voltar {
    width: 300px;
    padding: 10px;
    font-size: 1.5rem;
    margin-top: 20px;
    text-transform: uppercase;
    font-weight: 600;
    background: rgb(255, 0, 0);
    border: 2px solid rgb(255, 0, 0);
    border-radius: 15px;
    cursor: pointer;
    font-family: fantasy;
    color: black;
    transition: 0.2s;
}

.btn-voltar:hover {
    background: rgb(200, 0, 0);
    transform: scale(1.05);
}
</style>
