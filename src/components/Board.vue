<template>
  <div class="board" v-if="cards.length">
    <Card
        v-for="(card, i) in cards"
        :key="i"
        :card="card"
        :values="values"
        @flipped="onFlipped"
        @flipCard="onFlipCard"
    />
  </div>
</template>

<script>
  import Card from "./Card";

  export default {
    name: "Board",
    components:{ Card },
    data(){
      return {
        lastCard: null,
        values: ['apple', 'banana', 'lemon', 'pear', 'pineapple', 'cherry', 'strawberry', 'paprika', 'carrot', 'eggplant', 'tomato', 'onion'],
        cards:[],
      }
    },
    computed:{
      isAllMatched(){
        return this.cards.filter(c => c.isMatch).length;
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
          .filter(c => cards.includes(c))
          .forEach(c => c.flipped = !c.flipped);
      },
      start(){
        const cc = [...this.values, ...this.values].map(this.makeCard);
        this.cards = this.shuffle(cc)
      },
      makeCard(card){
        return {
          value: card,
          flipped: false,
          isMatch: false,
        }
      },
      shuffle(cards) {
        return cards.sort(() => Math.random() - 0.5);
      }
    },
    created(){
      this.start()
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
    display: grid;
    grid-template-rows: 1fr 1fr 1fr 1fr;
    grid-template-columns: repeat(4, minmax(1%, 1fr));
    max-width: 900px;
    height: calc(100vh - 200px);
    gap: 10px;
  }
  .wrapper:nth-child(4n) {
    margin-right: 0px;
  }

  @media screen and (max-width: 450px) {
    .board {
      width: 100%;
      height: calc(100vh - 50px);
      gap: 0;
    }
  }
</style>
