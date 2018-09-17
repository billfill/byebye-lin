<template>
  <div class="Hito" :style="{backgroundImage: 'url(' + srcRWD(bg, bg_p) + ')'}">
    <div class="title-wrapper" :class="{'title-left': isOpacityEnd}">
      <h1>這是一個快樂的標題</h1>
    </div>
    <div class="hito-section" :class="{'hito-opacity': hitoBgOpacity}"
         @transitionend.stop="handle_hitoSectionEnd">
      <div class="hito-wrapper" @click="resetHito" :class="{fadeOut: !hitoOpacity}">
        <img class="hito-hitotsu"
             :src="hito05" :class="{'hito-reset': toReset}"
             @transitionend.stop="handle_hitoEnd">
        <img class="hito-futatsu"
             :src="hito04" :class="{'hito-reset': toReset}"
             @transitionend.stop="handle_hitoEnd">
        <img class="hito-mittsu"
             :src="hito03" :class="{'hito-reset': toReset}"
             @transitionend.stop="handle_hitoEnd">
        <img class="hito-yottsu"
             :src="hito02" :class="{'hito-reset': toReset}"
             @transitionend.stop="handle_hitoEnd">
        <img class="hito-itsutsu"
             :src="hito01" :class="{'hito-reset': toReset}"
             @transitionend.stop="handle_hitoEnd">
      </div>
    </div>
  </div>
</template>

<script>
import srcRWD from '@/mixin/srcRWD.js'
import hito01 from '@/assets/hito01.png'
import hito02 from '@/assets/hito02.png'
import hito03 from '@/assets/hito03.png'
import hito04 from '@/assets/hito04.png'
import hito05 from '@/assets/hito05.png'
import bg from '@/assets/mobile_bg.jpg'
import bg_p from '@/assets/web_bg.jpg'
export default {
  name: 'Hito',
  mixins: [srcRWD],
  data () {
    return {
      bg: bg,
      bg_p: bg_p,
      hito01: hito01,
      hito02: hito02,
      hito03: hito03,
      hito04: hito04,
      hito05: hito05,
      toReset: false,
      hitoOpacity: true,
      hitoBgOpacity: false,
      isOpacityEnd: 0
    }
  },
  methods: {
    resetHito () {
      this.toReset = true
    },
    handle_touch () {
      
    },
    handle_hitoEnd () {
      this.hitoBgOpacity = true
    },
    handle_hitoSectionEnd () {
      console.log('trick')
      this.hitoOpacity = 0
      this.isOpacityEnd = true
    }
  },
  mounted () {

  }
}
</script>

<style lang="scss" scoped>
.Hito{
  position: relative;
  width: 100%;
  height: 100vh;
  background-color: #fff;
  overflow: hidden;
  background-repeat: no-repeat;
  background-size: 100% auto;
  background-position: left top;
  display: flex;
  justify-content: center;
  align-items: center;
}
.title-wrapper{
  position: absolute;
  z-index: 100;
  top: 0;
  left: 0;
  width: 100%;
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: transform 5000ms, opacity 1333ms;
  pointer-events: none;
  h1{
    position: relative;
    color: #fff;
    width: 1em;
    line-height: 1.3;
  }
}
.title-left{
  opacity: 1;
  transform: translate(-40%, 0);
  @media screen and (min-width: 1024px) {
    transform: translate(-25%, 0);
  }
}
.hito-section{
  position: absolute;
  z-index: 50;
  top: 0;
  left: 0;
  right: 0;
  bottom: 0;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(#000, 1);
  transition: background-color 3s ease-out;
}
.hito-opacity{
  background-color: rgba(#000, .3);
}
.hito-end{
  background-color: rgba(#000, 0);
}
.fadeOut{
  opacity: 0 !important;
}
.hito-wrapper{
  position: relative;
  width: 150px;
  height: 150px;
  transition: opacity 1s;
  @media screen and (min-width: 1024px) {
    width: 200px;
    height: 200px;
  }
  .hito-hitotsu{
    top: -100%;
    transform: translate(55%, -60%) rotate(405+720deg);
    @media screen and (min-width: 1024px) {
      transform: translate(-60%, 145%) rotate(0deg);
    }
  }
  .hito-futatsu{
    top: -50%;
    transform: translate(15%, 60%) rotate(-35deg);
    @media screen and (min-width: 1024px) {
      transform: translate(-180%, -100%) rotate(0deg);
    }
  }
  .hito-mittsu{
    transform: translate(-55%, -100%) rotate(-15deg);
    @media screen and (min-width: 1024px) {
      transform: translate(-250%, 125%) rotate(0deg);
    }
  }
  .hito-yottsu{
    top: 50%;
    transform: translate(60%, 50%);
    @media screen and (min-width: 1024px) {
      transform: translate(150%, -145%) rotate(0deg);
    }
  }
  .hito-itsutsu{
    top: 100%;
    transform: translate(-80%, 50%);
    @media screen and (min-width: 1024px) {
      transform: translate(250%, 50%) rotate(0deg);
    }
  }
  .hito-reset{
    transform: translate(0, 0) rotate(0) scale(1) skew(0);
  }
  img{
    position: absolute;
    top: 0;
    left: 0;
    width: 100%;
    transition: transform 2.8s ease-out;
  }
}
</style>
