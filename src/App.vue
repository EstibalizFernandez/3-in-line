<template>
  <div id="app">
    <section>
      <h1>3 EN RAYA</h1>
      <h2 v-if="winner === null">¡Suerte! Que gane el mejor</h2>
      <h2 v-else-if="winner === 'X' || winner === 'O'">¡Enhorabuena {{winner}}, has ganado! ¿La revancha?</h2>
      <h2 v-else>¡Ups! parece que no hay ganador ¿Queréis volver a intentarlo?</h2>
      <button @click="reset">REINICIAR</button>
    </section>

    <!-- Tablero -->
    <table align="center" border="1">
      <tr>
        <td @click="changeCell(0)">{{celdas[0]}}</td>
        <td @click="changeCell(1)">{{celdas[1]}}</td>
        <td @click="changeCell(2)">{{celdas[2]}}</td>
      </tr>
      <tr>
        <td @click="changeCell(3)">{{celdas[3]}}</td>
        <td @click="changeCell(4)">{{celdas[4]}}</td>
        <td @click="changeCell(5)">{{celdas[5]}}</td>
      </tr>
      <tr>
        <td @click="changeCell(6)">{{celdas[6]}}</td>
        <td @click="changeCell(7)">{{celdas[7]}}</td>
        <td @click="changeCell(8)">{{celdas[8]}}</td>
      </tr>
    </table>
  </div>
</template>

<script>

export default {
  name: 'inline',
  components: {
  },
  data() {
    return {
      winner: null,
      player: 'X',
      celdas: [null, null, null, null, null, null, null, null, null],
    }
  },
  watch: {
    player(newPlayer) {
      this.player = newPlayer;
    },
    celdas(newCells) {
      this.celdas = newCells; 
    },
    winner(newWinner) {
      this.winner = newWinner;
    }
  },
  mounted() {
    this.reset();
  },
  methods: {
    changeCell(number) {
      this.changeCells(number);
    },
    changeCells(number) {
      this.celdas.splice(number, 1, this.player);
      this.checkWinner();
    },
    changePlayer() {
      if (this.player == 'X') {
        this.player = 'O';
      } else {
        this.player = 'X';
      }
    },
    checkWinner() {
      if ( (this.celdas[0] !== null && this.celdas[0] === this.celdas[1] && this.celdas[0] === this.celdas[2]) 
      || (this.celdas[3] !== null && this.celdas[3] === this.celdas[4] && this.celdas[3] === this.celdas[5])
      || (this.celdas[6] !== null && this.celdas[6] === this.celdas[7] && this.celdas[6] === this.celdas[8])
      || (this.celdas[0] !== null && this.celdas[0] === this.celdas[4] && this.celdas[0] === this.celdas[8])
      || (this.celdas[2] !== null && this.celdas[2] === this.celdas[4] && this.celdas[2] === this.celdas[6])   
      || (this.celdas[0] !== null && this.celdas[0] === this.celdas[3] && this.celdas[0] === this.celdas[6]) 
      || (this.celdas[1] !== null && this.celdas[1] === this.celdas[4] && this.celdas[1] === this.celdas[7]) 
      || (this.celdas[2] !== null && this.celdas[2] === this.celdas[5] && this.celdas[2] === this.celdas[8]) ) {
        this.winner = this.player;
      } else if (
        this.celdas[0] !== null && this.celdas[1] !== null && this.celdas[2] !== null 
        && this.celdas[3] !== null && this.celdas[4] !== null  && this.celdas[5] !== null 
        && this.celdas[6] !== null && this.celdas[7] !== null && this.celdas[8] !== null
      ) {
        this.winner = 'ninguno';
      }
      this.changePlayer();
    },
    reset() {
      this.winner = null;
      this.player = 'X';
      this.celdas = [null, null, null, null, null, null, null, null, null];
    }
  },
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #7d7d7d;
  margin-top: 60px;

  h1 {
    color: #29ddb9;
  }

  section {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }

  button {
    margin-left: 15px;
    background-color: #7d7d7d;
    color: #fff;
    width: 80px;
    height: 30px;
    border: 2px solid #7d7d7d;
    border-radius: 5px;
    padding: 10px;
    display: flex;
    flex-direction: row;
    justify-content: center;
    align-items: center;
    margin-bottom: 10px;
    cursor: pointer;
  }

  table {
    border-spacing: 0px;
    border: 2px solid #29ddb9;
    td {
      width: 100px;
      height: 100px;
      border: 1px solid #29ddb9;
    }

  }
}
</style>
