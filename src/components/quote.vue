<template lang="pug">
.quote
  .quote__sentence {{ quote }}
  .quote__author {{ info }}
    span.author {{ author }}
    span
      i.icon(@click="updatelikedQuoteLocal()" :class="{ 'icon-heart-o': !likedQuote, 'icon-heart': likedQuote }")
      a(href='https://twitter.com/intent/tweet?url=http%3A%2F%2Fhelene-andre.github.io/Momentum%2F&text=Awesome+web+app!&hashtags=coolwebapp', target='_blank')
        i.icon.icon-twitter
</template>

<script>
export default {
  data: () => ({
    quote: '',
    author: '',
    info: null,
    likedQuote: 0
  }),
  mounted () {
    const axios = require('axios')
    axios
      .get('https://quotes.rest/qod')
      .then(response => (this.getQuoteOfTheDay(response)))
      .catch(() => {this.getQuoteOfTheDay()})

    this.likedQuote = localStorage.likedQuote === '0'
  },
  methods: {
    updatelikedQuoteLocal () {
      this.likedQuote = !this.likedQuote
      localStorage.likedQuote = this.likedQuote
    },
    getQuoteOfTheDay (response) {
      if (response) {
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
.quote {
  position: absolute;
  bottom: 12px;
  left: 50%;
  transform: translateX(-50%);
  width: 65%;
  text-align: center;
  font-size: 16px;
  padding: 10px;
  text-align: center;
  &__author {
    position: relative;
    width: 100%;
    opacity: 0;
    transition: all 0.3s ease-in-out;
    & .author {
      opacity: 0.7;
      font-size: 13px;
    }
    & span, & i {padding: 0 2px 0 2px;}
    & .icon-heart-o {
      opacity: 0.7;
      &:hover {opacity: 1;}
    }
  }
  &__sentence {
    position: absolute;
    width: 100%;
    transform: translateY(-10px);
    transition: all 0.3s ease-in-out;
  }
  &:hover {
    & .quote__author {
      opacity: 1;
      transform: translateY(3px);
    }
    & .quote__sentence {transform: translateY(-100%);}
  }
}

//=============================== media queries =====================================//
@media screen and (max-width: 1050px) {
  .quote{width: 50%;}
}

@media screen and (max-width: 800px) {
  .quote{width: 40%;}
}

@media screen and (max-width: 700px) {
  .quote{width: 30%;}
}

@media screen and (max-width: 500px) {
  .quote{width: 20%;}
}
//===================================================================================//
</style>

