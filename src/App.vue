<template>
  <div id="app">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view/>
  </div>
</template>

<style lang="sass">
$mxn: #89C053
$btc: #EBC256
$eth: #7F669F
html
  height: 100%
body
  color: #FFF 
  background-color: #272728
  background-image: -webkit-repeating-radial-gradient(center center,rgba(0,0,0,.1),rgba(0,0,0,.1) 1px,transparent 0,transparent 100%)
  background-image: repeating-radial-gradient(center center,rgba(0,0,0,.1),rgba(0,0,0,.1) 1px,transparent 0,transparent 100%)
  background-size: 4px 4px
  background-attachment: fixed
  overflow-x: hidden
h1, h2, h3, p
  color: #FFF 
#app
  font-family: 'Avenir', Helvetica, Arial, sans-serif
  -webkit-font-smoothing: antialiased
  -moz-osx-font-smoothing: grayscale
  text-align: center
  color: #2c3e50
#nav
  padding: 30px
  a
    font-weight: bold
    color: #FFF
    &.router-link-exact-active
      color: #FFF
.mxn 
  color: $mxn
.btc 
  color: $btc
.eth 
  color: $eth
</style>
