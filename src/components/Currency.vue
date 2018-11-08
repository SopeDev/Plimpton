<template>
  <span>{{ display }}</span>
</template>

<script>
export default {
  name: 'Currency',
  props: [
    'currency',
    'volume'
  ],
  methods: {
    roundCrypto (val) {
      return parseFloat(Math.round(val * 100000000) / 100000000).toFixed(8)
    }
  },
  computed: {
    display: function () {
      switch (this.currency) {
        case 'mxn':
          return '$ ' + parseFloat(Math.round(this.volume * 100) / 100).toFixed(2)
        case 'btc':
          return this.roundCrypto(this.volume) + ' BTC'
        case 'eth':
          return this.roundCrypto(this.volume) + ' ETH'
      }
    }
  },
}
</script>