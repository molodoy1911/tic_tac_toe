<script>
  import customInput from "@/components/CustomInput.vue";

  export default {
    components: {
      customInput
    },
    data() {
      return {
        field: [{id: 1, symbol: ""},{id: 2, symbol: ""},{id: 3, symbol: ""},
          {id: 4, symbol: ""},{id: 5, symbol: ""},{id: 6, symbol: ""},
          {id: 7, symbol: ""},{id: 8, symbol: ""},{id: 9, symbol: ""}],
        currentSymbol: "X",
        gridSize: 3
      }
    },
    computed: {
      winner() {
        const f = this.field;
        const size = this.gridSize;
        for (let i = 0; i < size; i++) {
          // проверка строки
          if (f[i * size].symbol && f.slice(i * size, i* size + size).every(cell => cell.symbol === f[i * size].symbol)) {
            return f[i * size].symbol;
          }
          // проверка столбца
          const column = [f[i], f[i + size], f[i + 2 * size]];
          if (column[0].symbol && column.every(cell => cell.symbol === column[0].symbol)) {
            return column[0].symbol;
          }
        }

        // проверка диагоналей
        const mainDiagonal = [f[0], f[4], f[8]];
        if (mainDiagonal[0].symbol && mainDiagonal.every(cell => cell.symbol === mainDiagonal[0].symbol)) {
          return mainDiagonal[0].symbol;
        }
        const antiDiagonal = [f[2], f[4], f[6]];
        if (antiDiagonal[0].symbol && antiDiagonal.every(cell => cell.symbol === antiDiagonal[0].symbol)) {
          return antiDiagonal[0].symbol;
        }

        return  null;
      }
    },
    methods: {
      select(cell) {
        if (cell.symbol === "" && !this.winner) {
          cell.symbol = this.currentSymbol;
          this.currentSymbol = this.currentSymbol === "X" ? "O" : "X";
        }
      }
    },
  }
</script>

<template>
  <div>
    <div class="grid">
      <div v-for="cell in field" :key="cell.id" class="cell">
        <custom-input :cell="cell" @select="select"></custom-input>
      </div>
    </div>
    <p v-if="winner" class="winner-message">Победил {{ winner}}!</p>
  </div>
</template>

<style>
.grid {
  display: grid;
  grid-template-columns: repeat(3, 50px);
  gap: 5px;
  justify-content: center;
  margin-top: 50px;
  margin-bottom: 30px;
  border: 3px solid #444;
  border-radius: 10px;
  padding: 10px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.2);
}

.cell {
  display: flex;
  justify-content: center;
  align-items: center;
  width: 50px;
  height: 50px;
  background-color: #f4f4f4;
  border-radius: 5px;
  cursor: pointer;
  font-size: 24px;
  transition: background-color 0.3s ease;
}

.cell:hover {
  background-color: #d4e4d9;
}

.winner-message {
  margin-top: 20px;
  font-size: 24px;
  color: #ff8c00;
  font-weight: bold;
  text-align: center;
  animation: fadeIn 2s ease-in-out;
}

@keyframes fadeIn {
  0% {
    opacity: 0;
    transform: translateY(20px);
  }
  100% {
    opacity: 1;
    transform: translateY(0);
  }
}
</style>