<template>
  <div id="app">
    <Feed />
  </div>
</template>

<script>
import Feed from './components/Feed'

export default {
  name: 'app',
  components: {
    Feed
  }
}
</script>

<style>
  body {
    margin: 0;
  }
  * {
    box-sizing: border-box;
  }

  #app {
    font-family: "Avenir", Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    background-color: #f9f9f9;
    padding-top: 30px;
  }
</style>
