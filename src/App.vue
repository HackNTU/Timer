<template>
  <div id="app">
    <!-- Get started by creating your first component: https://github.com/HackNTU/Timer/commit/ff81a21c5bd030dfc04d651d5b516f10723a976e -->
    <!-- <newcomponent></newcomponent> -->
    <section class="split-left">
      <countdown deadline="Sun Mar 19 2017 14:00:00 GMT+0800 (CST)" id="countdown"></countdown>
    </section>
    <section class="split-right">
      <h1>.split-right</h1>
    </section>
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

.split-left{
  border: 1px dashed red;
  position: fixed;
  top: 0;
  left: 0;
  width: 75vw;
  height: 100vh;
}

.split-right{
  border: 1px dashed blue;
  position: fixed;
  top: 0;
  right: 0;
  width: 25vw;
  height: 100vh;
}
</style>
