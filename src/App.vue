<template>
  <div id="app">
    <tasksManager />
  </div>
</template>

<script>
import tasksManager from './components/tasksManager.vue'

export default {
  name: 'App',
  components: {
    tasksManager
  }
}
</script>

<style lang="scss">
body {
    width: 100vw;
    height: 100vh;
    overflow: hidden;
}    
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 20px;
  height: 100%;
}
</style>
