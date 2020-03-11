<template lang="pug">
  .background
    img.background__image(alt="Vue logo" :src="getBackground()")

    .bottom-left-wrapper
      settings
      div
        .background__location {{ backgroundLocation }}
        .background__author
          a(:href="backgroundLink" target="_blank") Photo by {{ backgroundAuthor }}
          span.icon-heart-o

</template>

<script>
import settings from '../components/settings.vue'
export default {
  name: 'background',
  // props: {
  //   msg: String
  // }
  components: {settings},
  data: () =>({
    show: true,
    backgroundAuthor: '',
    backgroundLocation: '',
    backgroundLink: '',
    backgroundImages: [
      {
        author: 'Nick Cooper',
        location: 'Morskie Oko, Poland',
        src: 'background-image-0.jpg',
        href: 'https://unsplash.com/@cooper301'
      },
      {
        author: '',
        location: 'City of Bristol, United Kingdom',
        src: 'background-image-1.jpg',
        href: 'https://unsplash.com/@m_gatus'
      },
      {
        author: 'Sven Piek',
        location: 'Byron Bay NSW, Australia',
        src: 'background-image-1.jpg',
        href: 'https://unsplash.com/@sven_piek'
      },
      {
        author: 'Claudio Testa',
        location: 'Haselschacher Buck, Vogtsburg, Germany',
        src: 'background-image-2.jpg',
        href: 'https://unsplash.com/@claudiotesta'
      },
      {
        author: 'Eberhard Grossgasteiger',
        location: 'Mühlwald, South Tyrol, Italy',
        src: 'background-image-3.jpg',
        href: 'https://unsplash.com/@eberhardgross'
      },
      {
        author: 'Zach Reiner',
        location: 'Driftwood Beach Trail, Jekyll Island, United States',
        src: 'background-image-4.jpg',
        href: 'https://unsplash.com/@_zachreiner_'
      }
    ]
  }),
  methods: {
    getBackground() {
      let randomNumber = Math.floor(Math.random() * this.backgroundImages.length)

      this.backgroundAuthor = this.backgroundImages[randomNumber].author
      this.backgroundLocation = this.backgroundImages[randomNumber].location
      this.backgroundLink = this.backgroundImages[randomNumber].href
      return require(`../assets/images/${this.backgroundImages[randomNumber].src}`)
    }
  }
}
</script>

<style lang="scss">
.bottom-left-wrapper {
  display: flex;
  width: fit-content;
  position: fixed;
  left: 13px;
  bottom: 5px;
  padding-bottom: 7px;
}

.background {
  &__image {
    min-width: 100%;
    max-height: 100vh;
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    bottom: 0;
    z-index: -1;
  }
  &__location {
    opacity: 0.7;
    padding-bottom: 3px;
  }
  &__author {
    font-size: 11px;
    & span {
      padding-left: 5px;
      vertical-align: sub;
      font-size: 15px;
      opacity: 0;
      transition: 0.1s ease-in-out;
    }
    &:hover span {
      opacity: 0.6;
    }
    & span:hover {opacity: 1;}
  }
}

</style>