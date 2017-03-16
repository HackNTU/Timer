<template>
  <div id="app">
    <!-- Get started by creating your first component: https://github.com/HackNTU/Timer/commit/b0dc3586375a9a6a1ef7fdaf11628a391c4e6162 -->
    <newcomponent></newcomponent>
  </div>
</template>

<script>
import NewComponent from './components/NewComponent.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    newcomponent: NewComponent,
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
