<template>
  <div id="app">
    <img class="logo" alt="zjubca logo" src="./assets/logo.png">
    <h2>EOS区块链资源加油站</h2>
    <Home/>
    <div id="particles">
    </div>
  </div>
</template>

<script>
  import Home from './components/Home.vue'

  export default {
    name: 'app',
    components: {
      Home
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
  }

  .logo {
    margin-top: 60px;
    width: 180px;
  }

  #particles {
    position: absolute;
    top: 0;
    z-index: -999;
    width:100%;
    height: 100%;
    background-color: #fefefe;
    background-repeat: no-repeat;
    background-size: cover;
  }
</style>
