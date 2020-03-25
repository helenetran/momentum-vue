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
    this.getTime()
    setInterval(() => {
      this.getTime()
    }, 60000)
  },
  methods: {
    getTime () {
      let today = new Date()
      let hours = today.getHours() < 10 ? '0' + today.getHours() : today.getHours()
      let minutes = today.getMinutes() < 10 ? '0' + today.getMinutes() : today.getMinutes()

      document.getElementById("hours").innerHTML = hours
      document.getElementById("minutes").innerHTML = minutes

      // greetingMessage(hours)
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

