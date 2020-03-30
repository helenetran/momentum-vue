<template lang="pug">
#clock
  span#hours ..
  span.two-points :
  span#minutes ..
</template>

<script>
export default {
  name: 'clock',
  mounted () {
    this.showTime()
    setInterval(() => {
      this.showTime()
    }, 60000)
  },
  props: ['time'],
  methods: {
    showTime () {
      // console.log(this.time.minutes)
      document.getElementById("hours").innerHTML = this.time.hours
      document.getElementById("minutes").innerHTML = this.time.minutes
    }
  }
}
</script>

<style lang="scss">
#clock {
  font-size: 13em;
  font-weight: 600;
}
</style>

