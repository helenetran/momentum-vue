<template lang="pug">
.greeting
  .greeting__message(v-if="hours >= 5 && hours < 12") Good morning,
  .greeting__message(v-else-if="hours >= 12 && this.hours < 18") Good afternoon,
  .greeting__message(v-else) Good evening,
  pre &nbsp;
  .greeting__username(
    spellcheck='false'
    contenteditable=''
    @keydown.enter="$event.target.blur()"
    @keyup="checkUsername"
    @focus="animFocus"
    @blur="animBlur"
    :class="{ 'empty': noUserName, 'highlight': highlight, 'focus': focus }")
  span .
</template>

<script>
export default {
  name: 'greeting',
  props: ['hours', 'minutes'],
  data: () =>({
    timeoutDuration: 0,
    noUserName: true,
    usernameInput: '',
    greetingMessage: 'Hello',
    highlight: false,
    focus: false
  }),
  methods: {
    checkUsername () {
      this.usernameInput = document.getElementsByClassName('greeting__username')[0].innerHTML
      localStorage.username = this.usernameInput
      if (localStorage.username) {
        this.noUserName = false
        this.usernameInput = localStorage.username
      }
      else this.noUserName = true
    },
    animFocus () {
      this.highlight = true
      this.focus = true
      setTimeout(() => {this.highlight = false}, 300)
    },
    animBlur () {
      this.highlight = true
      this.focus = false
      setTimeout(() => {this.highlight = false}, 300)
    }
  }
}
</script>

<style lang="scss">
/*============================== greeeting ================================*/
.greeting {
  margin: 10px;
  display: flex;
  justify-content: center;
  &__message {text-align: right;}
  &__username {
    position: relative;
    display: block;
    color: white;
    font-weight: normal;
    font-family: Roboto, Arial, Helvetica, sans-serif;
    font-size: inherit;
    border: none;
    background-image: none;
    background-color: transparent;
    box-shadow: none;
    max-width: 350px;
    min-width: 50px;
    outline: none;
    cursor: auto;
    transition: 0.3s ease-out;
    border-radius: 3px;
    &.empty:after {content: "what's your name?";}
    &.empty + span {display: none}
    &.focus:after {display: none;}
    &:focus:before {
      content: '';
      position: absolute;
      top: 100%;
      left: 0;
      right: 0;
      border-bottom: 2px solid #fff;
    }
    &.highlight {
      background: rgba(255, 255, 255, 0.4);
      transition: 0.1s ease-in;
    }
  }
}



::placeholder {color: #fff;}
/*=========================================================================*/

/*========================= media queries =================================*/
@media screen and (max-height: 720px) {
  .greeting {
  font-size: 3.5em;
  width: unset;
  }
}

@media screen and (max-width: 750px) {
  .greeting {top: 35%;}
}

@media screen and (max-width: 670px) {
  .greeting {
    display: block;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }
  .greeting__message, .greeting__username {text-align: center;}
  .greeting__message {width: 100%;}
  .greeting__username {
  position: absolute;
    left: 50%;
    transform: translateX(-50%);
  }
}

@media screen and (max-height: 620px) {
  .greeting {font-size: 3.3em;}
}

@media screen and (max-height: 550px) {
  .greeting {font-size: 3em;}
}

@media screen and (max-height: 393px) {
  .greeting {
  width: 600px;
  transform: translateX(-50%);
  font-size: 3em;
  top: -23%;
  }
}

@media screen and (max-height: 330px) {
  .greeting {top: -33%;}
}

@media screen and (max-height: 270px) {
  .greeting {top: -42%;}
}

@media screen and (max-width: 620px) {
  .greeting {width: 420px;}
}

@media screen and (max-width: 500px) {
  .greeting {font-size: 2.2em;}
}
/*=========================================================================*/

</style>

