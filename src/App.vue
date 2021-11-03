<template>
  <div id="app">
    <Catalogo />
  </div>
</template>

<script>
import Catalogo from './components/Catalogo.vue'

export default {
  name: 'App',
  components: {
    Catalogo
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(41, 41, 41);
  color: rgb(235, 235, 235);
  overflow: hidden;
}
</style>