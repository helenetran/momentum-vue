<template lang="pug">
  #app
    background

    .middle-block
      clock
      greeting
    //- <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
</template>

<script>
import background from './components/background.vue'
import clock from './components/clock.vue'
import greeting from './components/greeting.vue'

export default {
  name: 'App',
  components: { background, clock, greeting }
}
</script>

<style lang="scss">
@import './sass/main.scss';

#app {
  height: 100vh;
}

.middle-block {
  position: absolute;
  top: 36%;
  left: 50%;
  transform: translateX(-50%);
}
</style>
