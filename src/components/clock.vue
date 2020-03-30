<template lang="pug">
#clock
  span {{ hours }}
  span :
  span {{ minutes }}
</template>

<script>
export default {
  props: ['hours', 'minutes']
}
</script>

<style lang="scss">
#clock {
  font-size: 13em;
  font-weight: 600;
}
</style>

