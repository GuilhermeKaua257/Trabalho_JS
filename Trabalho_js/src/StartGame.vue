<template>
   
    <div class="container">


        <div class="titulo">
            <h1>JOKENPÔ</h1>
        </div>

        <div class="box-btn">
            <button @click="SelectGame" class="btn" value="SelectPlayer">New Game</button>
            <button @click="SelectGame" class="btn " value="ArenaGame">continue Game</button>
        </div>
    </div>
</template>
<script>


export default {
    name: "StartGame",
    data() {
        return {
           select:""
        }
    },
    methods: {
        SelectGame(event) {
            const select = event.currentTarget.value;
            console.log(select);
            this.$emit('update:Select-game', select);
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
    border: 2px solid rgb(255, 0, 0);
    border-radius: 15px;
    color: rgb(0, 0, 0)
}
.btn:hover {
    transform: scale(1.05);
    background: rgb(200, 0, 0);
}

.titulo{
     color: rgb(0, 0, 0);
    font-size: 65px;
    text-align: center;
    font-family: fantasy;
}

</style>