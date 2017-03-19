<template>
  <div id="countdown">

    <div class="block">
      <p class="digit">{{ days | non_negtive }}</p>
      <p class="text">Days</p>
    </div>
    <div class="block">
      <p class="digit">{{ hours | non_negtive | two_digits }}</p>
      <p class="text">Hours</p>
    </div>
    <div class="block">
      <p class="digit">{{ minutes | non_negtive | two_digits }}</p>
      <p class="text">Minutes</p>
    </div>
    <div class="block">
      <p class="digit">{{ seconds | non_negtive | two_digits }}</p>
      <p class="text">Seconds</p>
    </div>

  </div>
</template>

<script>
export default {

  name: 'countdown',

  mounted: function() {
    window.setInterval(() => {
      this.now = Math.trunc((new Date()).getTime() / 1000);
    },1000);
  },

  props: ['deadline'],

  data: function() {
    return {
      now: Math.trunc((new Date()).getTime() / 1000),
    }
  },

  filters: {
    two_digits: function (value) {
      if(value.toString().length < 2)
      {
        return "0"+value.toString();
      }
      return value.toString();
    },
    non_negtive: function (value) {
      if(value < 0){
        return 0;
      }
      return value;
    }
  },

  computed: {
    normalizedDate: function() {
      return Math.trunc(Date.parse(this.deadline) / 1000);
    },
    seconds() {
      return (this.normalizedDate - this.now) % 60;
    },
    minutes() {
      return Math.trunc((this.normalizedDate - this.now) / 60) % 60;
    },
    hours() {
      return Math.trunc((this.normalizedDate - this.now) / 60 / 60) % 24;
    },
    days() {
      return Math.trunc((this.normalizedDate - this.now) / 60 / 60 / 24);
    },
  }
}

</script>

<style lang="css">
@import url(https://fonts.googleapis.com/css?family=Roboto+Condensed:400|Roboto:100);
.block {
  display: flex;
  flex-direction: column;
  margin: 2vw;
}
.text {
  color: #95989A;
  font-size: 2vw;
  font-family: 'Roboto Condensed', serif;
  font-weight: lighter;
  margin-top: 10px;
  margin-bottom: 10px;
  text-align: center;
}
.digit {
  color: #95989A;
  font-size: 10.5vw;
  font-weight: bold;
  font-family: 'Roboto', serif;
  margin: 1vw;
  text-align: center;
}
</style>
