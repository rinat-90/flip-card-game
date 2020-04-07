<template>
  <div>
    <img alt="Vue logo" src="./assets/logo.png">
    <Board />
  </div>
</template>

<script>

  import Board from "./components/Board";
  export default {
    name: 'App',
    components: {
      Board
    }
  }
</script>

<style>
  @import "./assets/index.css";
</style>
