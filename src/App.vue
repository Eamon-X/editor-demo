<template>
  <div id="app">
    <!-- <HelloWorld />
    <span>1</span> -->
    <Demo></Demo>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Demo from './components/Demo'

export default {
  name: 'App',
  components: {
    Demo,
    // HelloWorld,
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
