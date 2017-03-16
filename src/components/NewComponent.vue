<template lang="html">
<div class="green-box">
  <h1>{{msg}}</h1>
  <i>Find me in src/components/NewComponent.vue</i>
</div>
</template>

<script>
export default {
  name: 'newcomponent',
  data: function(){
    return{
      msg: 'hello <newcomponent>'
    }
  }

}
</script>

<style lang="css">
.green-box{
  border: green 1px solid;
}
</style>
