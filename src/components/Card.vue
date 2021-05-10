<template>
  <div class="wrapper" @click="flip">
    <div class="card" :class="{ flipped: card.flipped }" v-show="!card.isMatch">
      <img
          v-if="values.includes(card.value)"
          :src="require(`../assets/img/${card.value}.svg`)"
          :alt="card.value"
          class="front" />

      <img class="back" src="../assets/img/card.svg" />
    </div>
  </div>
</template>

<script>
  export default {
    props: {
      values: Array,
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
    width: 100%;
    height: 140px;
    cursor: pointer;
    position: relative;
    perspective: 800px;
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
      width: 100%;
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
