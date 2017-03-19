<template>
  <div id="app">
    <!-- Get started by creating your first component: https://github.com/HackNTU/Timer/commit/ff81a21c5bd030dfc04d651d5b516f10723a976e -->
    <!-- <newcomponent></newcomponent> -->

    <section class="top-left-fixed">
      <h1>2017台大黑客松，敬請期待！</h1>
    </section>
    <section class="split-left">
      <div id="opacity-bg"></div>
      <countdown deadline="Sat Jul 22 2017 09:00:00 GMT+0800 (CST)" id="countdown"></countdown>
    </section>
    <section class="split-right">
      <img id="logo" src="public/hackntu-logo.png" alt="hackntu logo">
      <agenda id="agenda"></agenda>
    </section>
  </div>
</template>

<script>
import NewComponent from './components/NewComponent.vue'
import Countdown from './components/Countdown.vue'
import Agenda from './components/Agenda.vue'
export default {
  name: 'app',
  data () {
    return {
      DDL: 'Sat Jul 22 2017 09:00:00 GMT+0800 (CST)',
    }
  },
  components: {
    newcomponent: NewComponent,
    countdown: Countdown,
    agenda: Agenda,
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
  display: flex;
  justify-content: center;
  left: 0;
  position: absolute;
  right: 0;
  top:0;
}

#agenda{
  /*border: 1px dashed pink;*/
}

.split-left{
  /*border: 1px dashed red;*/
  position: fixed;
  top: 0;
  left: 0;
  width: 74vw;
  height: 100vh;
}

.split-right{
  /*border: 1px dashed blue;*/
  position: fixed;
  top: 0;
  right: 0;
  width: 26vw;
  height: 100vh;
}

.top-left-fixed{
  /*border: 1px dashed green;*/
  position: fixed;
  top: 5vh;
  left: 5vw;
  /*height: 1em;*/
}

h1{
  color: #95989A;
  font-size: 2.5em;
  font-weight: lighter;
}

#logo{
  /*border: 1px dashed yellow;*/
  position: absolute;
  top: 35px;
  left: 50px;
  width: 18vw;
  /*margin: 50px;*/
}

/* CSS trick to creat transparent background */
/* https://css-tricks.com/snippets/css/transparent-background-images/ */
#opacity-bg {
  /*border: 1px green dashed;*/
  width: 75vw;
  height: 100vh;
  display: block;
  position: relative;
}
/*#opacity-bg::after {
  content: "";
  background: url(../public/logo.png);
  background-repeat: no-repeat;
  background-position: center 105%;
  opacity: 0.2;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  position: absolute;
  z-index: -1;
}*/
</style>
