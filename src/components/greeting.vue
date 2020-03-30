<template lang="pug">
.greeting
  .greeting__message
  .greeting__username.empty(spellcheck='false', contenteditable='' @keyup="checkUsername" @keypress="checkUsername")
  span .
</template>

<script>
export default {
  name: 'greeting',
  data: () =>({

  }),
  methods: {
    greetingMessage (currentHour) {
      let message = ''
      if (currentHour >= 5 && currentHour < 12) message = 'Good morning'
      else if (currentHour >= 12 && currentHour < 18) message = 'Good afternoon'
      else message = 'Good evening'
      document.getElementsByClassName('greeting__message')[0].innerHTML = message + ',&nbsp;'
    },

    checkUsername () {
    console.log('test')
    let usernameInput = document.getElementsByClassName('greeting__username')[0]
    if (localStorage.username) usernameInput.html(localStorage.username)
    usernameInput[localStorage.username ? 'removeClass' : 'addClass']('empty')

    usernameInput
      .on('keyup', function () {localStorage.username = this.innerHTML})
      .on('keypress', function (e) {if (e.which === 13) this.blur()})
      .on('focus', function () {
        usernameInput.addClass('focus highlight')
        setTimeout(function () {usernameInput.removeClass('highlight')}, 300)
      })
      .on('blur', function () {
        localStorage.username = this.innerHTML
        usernameInput.removeClass('focus')
        usernameInput[localStorage.username ? 'removeClass' : 'addClass']('empty')

        usernameInput.addClass('highlight')
        setTimeout(function () {usernameInput.removeClass('highlight')}, 300)
      })
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
}

.greeting__message {
	text-align: right;
}

.greeting__username {
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
}
.greeting__username.empty:after {content: "what's your name?";}
.greeting__username.empty + span {display: none}
.greeting__username.focus:after {display: none;}
.greeting__username:focus:before {
	content: '';
	position: absolute;
	top: 100%;
	left: 0;
	right: 0;
	border-bottom: 2px solid #fff;
}

.greeting__username.highlight {
	background: rgba(255, 255, 255, 0.4);
	transition: 0.1s ease-in;
}

::placeholder {color: #fff;}
/*=========================================================================*/

</style>

