<template lang="pug">
.greeting
  .greeting__message
  .greeting__username.empty(spellcheck='false', contenteditable='')
  span .
</template>

<script>
export default {
  name: 'greeting',
  data: () =>({

  }),
  methods: {

  }
}
</script>

<style lang="scss">
#clock {
  font-size: 13em;
  font-weight: 600;
}
</style>

