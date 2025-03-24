<script>
  export default {
    props: ["cell"],
    emits: ["select"]
  }
</script>

<template>
  <div class="cell_container" @click="$emit('select' ,cell)">
    <div class="cell_value">
      {{ cell.symbol }}
    </div>
  </div>
</template>

<style>
  .cell_container {
    height: 100%;
    width: 100%;
    border: 1px solid black;
  }

  .cell_value {
    width: 50px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    color: #333;
  }
</style>