<template>
  <div class="wrapper" @click="flip">
    <div class="card" :class="{ flipped: card.flipped }" v-show="!card.isMatch">
      <img v-if="card.value === 'apple'" class="front" src="../assets/img/apple.svg" />
      <img v-if="card.value === 'banana'" class="front" src="../assets/img/banana.svg" />
      <img v-if="card.value === 'lemon'" class="front" src="../assets/img/lemon.svg" />
      <img v-if="card.value === 'pear'" class="front" src="../assets/img/pear.svg" />
      <img v-if="card.value === 'pineapple'" class="front" src="../assets/img/pineapple.svg" />
      <img v-if="card.value === 'strawberry'" class="front" src="../assets/img/strawberry.svg" />
      <img v-if="card.value === 'carrot'" class="front" src="../assets/img/carrot.svg" />
      <img v-if="card.value === 'eggplant'" class="front" src="../assets/img/eggplant.svg" />
      <img v-if="card.value === 'onion'" class="front" src="../assets/img/onion.svg" />
      <img v-if="card.value === 'paprika'" class="front" src="../assets/img/paprika.svg" />
      <img v-if="card.value === 'tomato'" class="front" src="../assets/img/tomato.svg" />
      <img v-if="card.value === 'cherry'" class="front" src="../assets/img/cherry.svg" />


      <img class="back" src="../assets/img/card.svg" />
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      card: {
        type: Object,
        default() {
          return {
            flipped: false,
            value: ''
          }
        }
      }
    },
    methods:{
      flip(){
        if (this.card.flipped) return;
        this.$emit('flipCard', this.card);
        this.$emit('flipped', this.card)
      }
    }

  }
</script>

<style scoped>
  .wrapper {
    width: 100px;
    height: 150px;
    cursor: pointer;
    position: relative;
    perspective: 800px;
    display: inline-flex;
  }
  .card {
    width: 100%;
    height: 100%;
    transition: transform 1s;
    transform-style: preserve-3d;
  }

  .card.flipped {
    transform: rotateY(180deg);
  }

  .card img {
    display: block;
    height: 100%;
    width: 100%;
    position: absolute;
    backface-visibility: hidden;
  }

  .card .back {
    transform: rotateY(0deg);
  }

  .card .front {
    transform: rotateY(180deg);
  }

  @media screen and (max-width: 600px) {
    .wrapper {
      width: 90px;
      height: 150px;
      margin-right: 1px;
    }
  }

  @media screen and (max-width: 420px) {
    .wrapper {
      width: 80px;
      height: 150px;
      margin-right: 1px;
    }
  }

  @media screen and (max-width: 360px) {
    .wrapper {
      width: 80px;
      height: 94px;
      margin-right: 1px;
    }
  }
</style>