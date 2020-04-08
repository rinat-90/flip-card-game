<template>
  <div id="app">
    <div class="header">
      <div><a href="#" class="header-logo">Flip Card</a></div>
      <div><span class="num">tries: {{ num }}</span></div>
    </div>
    <Board @count="num++"  @start="num = 0"/>
  </div>
</template>

<script>
  import Board from "./components/Board";
  export default {
    name: 'App',
    components: { Board },
    data(){
      return {
        num: 0
      }
    }
  }
</script>

<style>

  #app{
    width: 600px;
    height: 100vh;
    border-radius: 2px;
    display: flex;
    flex-direction: column;
  }

  .header{
    display: flex;
    justify-content: space-between;
    margin-top: 10px;
    padding: 10px;
    color: #fff;
    background-color: #3d414d;
    border-radius: 2px;
  }

  .header-logo{
    text-decoration: none;
    text-transform: uppercase;
    color: #f1f1f1;
    font-weight: bold;
  }

  .num{
    color: grey;
  }

  .btn{
    padding: 3px 10px;
    outline: none;
    border: none;
    border-radius: 3px;
  }
</style>
