<template lang="pug">
  .settings
    //- Settings wheel.
    .icon-settings.settings__wheel(@click="showSettings(), show = !show")

    //- Settings popup.
    transition(name="fade")
      .settings__popup(v-if="show")

        //- Left block.
        .settings__popup--left
          ul
            li(v-for="item in listItems" :key="item.id" :class="item.class" @click="showParagraph(item.id)") {{ item.name }}
          .login
            .login__title Log In
            .login__description Sync your account & more!

        //- Right block.
        .settings__popup--right(v-for="item in listItems" :key="item.id")
          div(v-if="paragraphId === item.id") {{ item.name }}
</template>

<script>
export default {
  name: 'settings',
  // props: {
  //   msg: String
  // }
  data: () =>({
    show: false,
    paragraphId: 0,
    listItems: [
      {
        id: 0,
        name: 'General',
        class: 'list-item__medium',
        condition: 'paragraphId === 0'
      },
      {
        id: 1,
        name: 'Todo',
        class: 'list-item__medium'
      },
      {
        id: 2,
        name: 'Mantras',
        class: 'list-item__medium'
      },
      {
        id: 3,
        name: 'Photos',
        class: 'list-item__medium'
      },
      {
        id: 4,
        name: 'Quotes',
        class: 'list-item__medium'
      },
      {
        id: 5,
        name: 'Links',
        class: 'list-item__medium'
      },
      {
        id: 6,
        name: 'Balance',
        class: 'list-item__medium'
      },
      {
        id: 7,
        name: 'Help',
        class: 'list-item__small'
      },
      {
        id: 8,
        name: 'What\'s New',
        class: 'list-item__small'
      },
      {
        id: 9,
        name: 'About',
        class: 'list-item__small'
      },
      {
        id: 10,
        name: 'Upgrade to Plus',
        class: 'list-item__small'
      }
    ]
  }),
  methods: {
    showSettings() {
      let settingWheel = event.target
      settingWheel.classList.toggle("rotate")
    },
    showParagraph(paragraphIdClicked) {
      this.paragraphId = paragraphIdClicked
    }
  }
}
</script>

<style lang="scss">
.settings ul {width: 180px;}

.settings__wheel {
  text-align: center;
	height: 19px;
	width: 19px;
	padding: 0;
	margin: 0;
  position: relative;
  top: 50%;
  transform: translateY(-50%);
  padding: 0 13px 0 5px;
  font-size: 21px;
  opacity: 0.6;
  transition: 0.1s ease-in-out;
  &:hover {
    opacity: 1;
  }
}

.settings__popup {
  width: 700px;
  height: 450px;
  background-color: rgba(0, 0, 0, 0.8);
  border-radius: 5px;
  position: fixed;
  left: -12px;
  bottom: 5%;
  margin: 18px;
  font-size: 1.3em;
  display: flex;
}

.settings__popup:before {
  content: "";
  width: 0;
  height: 0;
  border: 7px solid transparent;
  border-top-color: rgba(0, 0, 0, 0.8);
  opacity: 0.9;
  position: absolute;
	left: 14px;
  top: 100%;
}

.settings__popup--left {
	display: flex;
	flex-direction: column;
	justify-content: space-between;
}


.list-item__medium {padding: 6px 21px;}
.list-item__small {
	padding: 5px 21px;
	font-size: 12px;
}

.settings__popup--left .login {
	height: 7%;
	padding: 15px 19px 19px;
	font-size: 13px;
	background: rgba(255, 255, 255, 0.1 );
}

.settings__popup--left .login__title {
	font-size: 14px;
}

.settings__popup--left .login__description {
	font-size: 10px;
	margin: 2px 0;
	opacity: 0.6;
}

//=============================== Animations ========================================//
.rotate {
  transform: translateY(-40%) rotate(40deg) scale(1.08);
  opacity: 1;
}

.fade-enter-active, .fade-leave-active {
  transition: all 0.3s ease-in-out;
}

.fade-enter, .fade-leave-to {
  opacity: 0;
  transform: translateY(10px);
}
//===================================================================================//
</style>