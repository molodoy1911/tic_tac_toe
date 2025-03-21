<script>
  export default {
    data() {
      return {
        field: [{id: 1, symbol: ""},{id: 2, symbol: ""},{id: 3, symbol: ""},
                {id: 4, symbol: ""},{id: 5, symbol: ""},{id: 6, symbol: ""},
                {id: 7, symbol: ""},{id: 8, symbol: ""},{id: 9, symbol: ""}],
        currentSymbol: "X",
        gameOver: false,
        winningCombinations: [
            [0, 1, 2], [3, 4, 5], [6, 7, 8],
            [0, 3, 6], [1, 4, 7], [2, 5, 8],
            [0, 4, 8], [2, 4, 6]
        ]
      }
    },
    methods: {
      putSymbol(cell) {
        if (cell.symbol === "" && !this.gameOver) {
          cell.symbol = this.currentSymbol;
          if (this.checkWinner()) {
            alert(`Победил ${this.currentSymbol}!`);
            this.gameOver = true;
          } else {
            this.currentSymbol = this.currentSymbol === "X" ? "O" : "X";
          }
        }
      },
      checkWinner() {
        return this.winningCombinations.some(combo => {
          const [a, b, c] = combo;
          return (
            this.field[a].symbol &&
            this.field[a].symbol === this.field[b].symbol &&
            this.field[a].symbol === this.field[c].symbol
          );
        });
      },
      resetGame() {
        this.field.forEach(cell => cell.symbol = "");
        this.currentSymbol = "X";
        this.gameOver = false;
      }
    }
  }
</script>

<template>
  <div>
    <div class="grid">
      <div v-for="cell in field" :key="cell.id" class="cell" @click="putSymbol(cell)">
        {{ cell.symbol }}
      </div>
    </div>
    <button @click="resetGame">Начать заново</button>
  </div>
</template>

<style>
  .grid {
    display: grid;
    grid-template-columns: repeat(3, 50px);
    gap: 5px;
  }
  .cell {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    border: 1px solid black;
  }
</style>