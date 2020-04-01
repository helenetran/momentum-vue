<template lang="pug">
  #app
    .middle-block
      clock(:hours="hours" :minutes="minutes")
      greeting(:hours="hours" :minutes="minutes")

    background
</template>

<script>
import background from './components/background.vue'
import clock from './components/clock.vue'
import greeting from './components/greeting.vue'

export default {
  name: 'App',
  components: { background, clock, greeting },
  data: () =>({
    hours: 0,
    minutes: 0,
    seconds: 0
  }),
  mounted () {
    this.getTime()

    // Number of seconds to snap the the real time minutes change.
    const timeoutDuration = (60 - this.seconds)

    setTimeout(() => {
      this.getTime()

      setInterval(
        () => {
          this.getTime()
        }, 60000)
    }, timeoutDuration * 1000)
  },
  methods: {
    getTime () {
      let now = new Date()
      this.hours = now.getHours() < 10 ? '0' + now.getHours() : now.getHours()
      this.minutes = now.getMinutes() < 10 ? '0' + now.getMinutes() : now.getMinutes()
      this.seconds = now.getSeconds() < 10 ? '0' + now.getSeconds() : now.getSeconds()
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
  width: 100%;
}
</style>
