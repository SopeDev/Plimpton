<template>
  <section class="transaction">
    <h2>{{ type }} <span :class="market.book[0]">{{ market.book[0] }}</span></h2>
    <h2 v-if="type === 'buy'" class="entry">
      <span :class="market.book[1]">
        <Currency :volume="volume * market.price" :currency="market.book[1]"/>
      </span>
      <i class="far fa-hand-point-right"></i>
      <span :class="market.book[0]">
        <Currency :volume="volume" :currency="market.book[0]"/>
        <small>(- 1%)</small>
      </span>
    </h2>
    <h2 v-else class="entry">
      <span :class="market.book[0]">
        <Currency :volume="volume" :currency="market.book[0]"/>
      </span>
      <i class="far fa-hand-point-right"></i>
      <span :class="market.book[1]">
        <Currency :volume="volume * market.price" :currency="market.book[1]"/>
        <small>(- 1%)</small>
      </span>
    </h2>
    <div :class="'price-line-container ' + type">
      <div class="price-line"></div>
      <span class="min"><Currency :volume="market.min" :currency="market.book[1]"/></span>
      <span class="media"><Currency :volume="market.mediaVal" :currency="market.book[1]"/></span>
      <span class="max"><Currency :volume="market.max" :currency="market.book[1]"/></span>
      <span class="price" v-bind:style="priceLineStyle"><Currency :volume="market.price" :currency="market.book[1]"/><span></span></span>
    </div>
  </section>
</template>

<script>
  import Currency from '@/components/Currency.vue'
export default {
  name: 'Transaction',
  components: { Currency },
  props: [
    'market',
    'type',
    'volume'
  ],
  computed: {
    priceLineStyle: function () {
      return { left: this.getPriceRangePercent(this.market.min, this.market.price, this.market.max) + '%' }
    }
  },
  methods: {
    getPriceRangePercent (min, val, max) {
      return (val - min) / (max - min) * 100
    }
  }
}
</script>

<style scoped lang="sass">
.transaction
  width: fit-content
  padding: 25px
  margin: auto
  background: rgba(0, 0, 0, 0.15)
  border-radius: 10px
  & + .transaction
    margin-top: 25px
  h2
    margin-top: 0
    text-transform: uppercase
    i
      font-size: 1rem 
      margin: 0 10px
    small
      margin-left: 10px
  .price-line-container
    position: relative 
    width: 600px
    padding-top: 45px
    margin: auto
    &.buy
      .price-line
        background: linear-gradient(to right, #008000, #2196F3, #F00)
      .min
        color: #008000 
      .max
        color: #F00 
    &.sell
      .price-line
        background: linear-gradient(to left, #008000, #2196F3, #F00)
      .min
        color: #F00
      .max
        color: #008000 
    .price-line
      width: 100%
      height: 15px
      margin-bottom: 4px
      border-radius: 5px
    .min
      float: left
    .media
      color: #2196F3
      font-weight: 600  
    .max
      float: right
    .price
      position: absolute
      display: flex
      width: fit-content 
      flex-direction: column
      align-items: center
      top: 0
      color: #FFF
      font-size: 1.5em 
      font-weight: 600
      transform: translate3d(-50%, 0, 0)
      span:nth-child(2)
        width: 0
        height: 0
        margin-top: 5px
        border-left: 5px solid transparent
        border-right: 5px solid transparent
        border-top: 5px solid #FFF
</style>
