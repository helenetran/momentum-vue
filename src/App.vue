<template lang="pug">
  #app
    .middle-block
      clock(:time='time')
      greeting

    background
    //- <!-- <HelloWorld msg="Welcome to Your Vue.js App"/> -->
</template>

<script>
import background from './components/background.vue'
import clock from './components/clock.vue'
import greeting from './components/greeting.vue'

export default {
  name: 'App',
  beforeMount () {
    this.getTime()
  },
  mounted () {
    // this.getTime()
    setInterval(() => {
      this.getTime()
    }, 1000)
  },
  components: { background, clock, greeting },
  data: () =>({
    time: {
      hours: 6,
      minutes: 0
    }
  }),
  methods: {
    getTime () {
      let today = new Date()
      this.time.hours = today.getHours() < 10 ? '0' + today.getHours() : today.getHours()
      this.time.minutes = today.getMinutes() < 10 ? '0' + today.getMinutes() : today.getMinutes()
      console.log(today, this.time.minutes)
    }
  }
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
