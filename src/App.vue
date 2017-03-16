<template>
  <div id="app">
    <!-- Get started by creating your first component: https://github.com/HackNTU/Timer/commit/b0dc3586375a9a6a1ef7fdaf11628a391c4e6162 -->
    <!-- <newcomponent></newcomponent> -->
    <countdown deadline="Sun Mar 19 2017 14:00:00 GMT+0800 (CST)" id="countdown"></countdown>
  </div>
</template>

<script>
import NewComponent from './components/NewComponent.vue'
import Countdown from './components/Countdown.vue'
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  },
  components: {
    newcomponent: NewComponent,
    countdown: Countdown,
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

#countdown {
  align-items: center;
  bottom: 0;
  /*background-color: #34495e;*/
  display: flex;
  justify-content: center;
  left: 0;
  position: absolute;
  right: 0;
  top:0;
}
</style>
