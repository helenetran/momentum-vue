<template lang="pug">
#quote(@mouseover="show = true" @mouseleave="show = false")
  transition(name="slide")
    .quote {{ quote }}
  transition(name="fade")
    .quote-author(v-if="show") {{ info }}
      span.author {{ author }}
      span
        i#like-quote.icon.icon-heart-o.icon-link
        a(href='https://twitter.com/intent/tweet?url=http%3A%2F%2Fhelene-andre.github.io/Momentum%2F&text=Awesome+web+app!&hashtags=coolwebsite', target='_blank')
          i#twitter.icon.icon-twitter.icon-link
</template>

<script>
export default {
  data: () => ({
    quote: '',
    author: '',
    info: null,
    show: false
  }),
  mounted () {
    const axios = require('axios')
    axios
      .get('https://quotes.rest/qod')
      .then(response => (this.getQuoteOfTheDay(response)))
  },
  methods: {
    getQuoteOfTheDay (response) {
        if (response.data.contents.quotes[0].quote) {
          this.quote = `“${response.data.contents.quotes[0].quote}”`
          this.author = response.data.contents.quotes[0].author
        }
        else {
          this.quote = '“Those who dare to fail miserably can achieve greatly.”'
          this.author = 'John F. Kennedy'
        }
    }
  }
}
</script>

<style lang="scss">
#quote {
  position: absolute;
  bottom: 0;
  left: 50%;
  transform: translateX(-50%);
  width: 70%;
  text-align: center;
  font-size: 15px;
}

.fade-enter-active, .fade-leave-active {
  transition: all 0.3s ease-in-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}
</style>

