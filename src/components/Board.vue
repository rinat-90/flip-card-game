<template>
  <div class="board" v-if="cards.length">
    <Card v-for="(card, i) in cards"
          :key="i"
          :card="card"
          @flipped="onFlipped"
          @flipCard="onFlipCard"/>
  </div>
</template>

<script>
  import Card from "./Card";

  export default {
    name: "Board",
    components:{ Card },
    computed:{
      isAllMatched(){
        return this.cards.filter(c => c.isMatch).length;
      }
    },
    created(){
      this.start()
    },
    data(){
      return {
        lastCard: null,
        values: ['apple', 'banana', 'lemon', 'pear', 'pineapple', 'cherry', 'strawberry', 'paprika', 'carrot', 'eggplant', 'tomato', 'onion'],
        cards:[]
      }
    },
    methods: {
      onFlipped(e){
        if (!this.lastCard) {
          return (this.lastCard = e)
        }
        if (this.lastCard !== e && this.lastCard.value === e.value) {
          this.$emit('count');
          const lastCard = this.lastCard;
          this.lastCard = null;

          setTimeout(()=> {
            lastCard.isMatch = true;
            e.isMatch = true
          },1000)

        }
        const lastCard = this.lastCard;
        this.lastCard = null;
        setTimeout(() => {
          this.flipCards([lastCard, e]);
          this.$emit('count');
        }, 1000);

      },
      onFlipCard(card){
        const c = this.cards.find(cc => cc === card);
        c.flipped = !c.flipped
      },
      flipCards(cards){
        this.cards
          .filter(c => cards.indexOf(c) >= 0)
          .forEach(c => c.flipped = !c.flipped);
      },
      start(){
        const cc = this.values.concat(this.values).map(this.makeCard);
        this.cards = this.shuffle(cc)
      },
      makeCard(card){
        return {
          value: card,
          flipped: false,
          isMatch: false
        }
      },
      shuffle(cards) {
        return cards.sort(() => Math.random() - 0.5);
      }
    },
    watch:{
      isAllMatched(val){
        if(val === 24){
          this.start();
          this.$emit('start');
        }
      }
    }
  }
</script>

<style scoped>
  .board{
    width: 100%;
    height: 100vh;
    background-color: #3d414d;
    margin-top: 10px;
    border-radius: 4px;
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    align-items: center;
    align-content: space-between;
  }
  .wrapper:nth-child(4n) {
    margin-right: 0px;
  }

  @media screen and (max-width: 450px) {
    .board {
      width: 100%;
      height: 100vh;
      justify-content: space-around;
    }
  }
</style>