<template>
  <div id="trade-room">
    <h1>
      <span class="mxn">MXN</span>
      <i class="far fa-hand-point-right"></i>
      <span class="btc">BTC</span>
      <i class="far fa-hand-point-right"></i>
      <span class="eth">ETH</span>
      <i class="far fa-hand-point-right"></i>
      <span class="mxn">MXN</span>
    </h1>
    <Transaction type="buy" :market="entryMarket" :volume="entry"/>
    <Transaction type="buy" :market="exitMarket" :volume="middle"/>
    <Transaction type="sell" :market="xchangeMarket" :volume="exit"/>
  </div>
</template>

<script>
import Transaction from '@/components/Transaction.vue'
export default {
  name: 'QuickExample',
  components: { Transaction },
  data () {
    return {
      entryMarket: {},
      exitMarket: {},
      xchangeMarket: {}
    }
  },
  computed: {
    entry: function () {
      return this.entryMarket.volume > this.exitMarket.val ? this.exitMarket.val : this.entryMarket.volume
    },
    middle: function () {
      return (this.entry / this.exitMarket.price) - (this.entry / this.exitMarket.price) * 0.01
    },
    exit: function () {
      return this.middle - this.middle * 0.01
    }
  },
  methods: {
    round(val, decimals) {
      return Number(Math.round(val+'e'+decimals)+'e-'+decimals);
    },
    getMedia (market) {
      return (market.max + market.min) / 2
    }
  },
  created () {
    this.entryMarket = {
      book: 'btc_mxn'.split('_'),
      max : 120749.98,
      min : 118276.37,
      price : 119330.00,
      volume : 0.06150244,
      val :  7339.09,
      mediaVal : null,
    }
    this.entryMarket.mediaVal = this.getMedia(this.entryMarket)

    this.exitMarket = {
      book: 'eth_btc'.split('_'),
      max : 0.03206135,
      min : 0.03076675,
      price : 0.03186871,
      volume : 0.00012727,
      val : 0.00000406,
      mediaVal : null,
    }
    this.exitMarket.mediaVal = this.getMedia(this.exitMarket)

    this.xchangeMarket = {
      book: 'eth_mxn'.split('_'),
      max : 3865.88,
      min : 3742.05,
      price :  3780.00,
      volume : 0.52910053,
      val :  2000.00,
      mediaVal : null,
    }
    this.xchangeMarket.mediaVal = this.getMedia(this.xchangeMarket)
  }
}
</script>

<style scoped lang="sass">
h1
  display: flex
  align-items: center
  justify-content: center
  i
    font-size: 1rem
    margin: 0 10px
h2
  span
    font-size: 1rem
    margin-left: 15px
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
    height: 4px
    margin-bottom: 4px
    border-radius: 100%
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
    flex-direction: column
    align-items: center
    top: 0
    color: #FFF
    font-size: 1.5em 
    font-weight: 600
    transform: translate3d(-50%, 0, 0)
    span
      width: 0
      height: 0
      margin-top: 5px
      border-left: 5px solid transparent
      border-right: 5px solid transparent
      border-top: 5px solid #FFF
</style>
