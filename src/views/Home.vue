<template>
  <div class="home">
    <div class="leftArrow" @mouseleave="transform" @click="leftMove"><button> 《 </button></div>
    <div class="app">
      <div class="container" :class="{transform: state.transform}" :style="{left: state.imgLeft + 'vw'}">
        <div  class="image" @mouseleave="transform" @mouseenter="noTransform" v-for="(item, index) in state.list" :key="index">
          <img :src="require('@/assets/img/' + item)" />
        </div>
      </div>
      <!-- <div class="dots">
        <div class="dot" :class="{active: index === state.currentPage}" v-for="(item, index) in state.list" :key="index">
        </div>
      </div> -->
    </div>
    <div class="rightArrow" @mouseleave="transform" @click="rightMove()"><button> 》 </button></div>
  </div>
</template>

<script lang="ts">
import { reactive } from 'vue'
export default {
  name: 'App',
  setup () {
    const state = reactive({
      list: ['1.jpg', '2.jpg', '3.jpg', '4.jpg', '5.jpg', '6.jpg', '7.jpg', '8.jpg', '9.jpg', '10.jpg', '11.jpg', '12.jpg', '13.jpg', '14.jpg', '15.jpg', '16.jpg', '1.jpg', '2.jpg', '3.jpg', '4.jpg'],
      imgLeft: 0,
      currentPage: 0,
      transform: true
    })

    var timer = setInterval(func, 4000)
    function func () {
      state.currentPage++
      changePic()
    }

    function changePic () {
      state.transform = true
      if (state.currentPage === 5) {
        state.currentPage = 0
        state.transform = false
      }
      if (state.currentPage === -1) {
        state.currentPage = 4
        state.transform = false
      }
      state.imgLeft = -80 * state.currentPage
    }

    function leftMove () {
      clearInterval(timer)
      state.currentPage--
      changePic()
    }

    function rightMove () {
      clearInterval(timer)
      state.currentPage++
      changePic()
    }

    function noTransform () {
      clearInterval(timer)
    }

    function transform () {
      timer = setInterval(func, 4000)
    }

    return {
      state,
      leftMove,
      rightMove,
      noTransform,
      transform
    }
  }
}
</script>

<style>
  .home {
    position: relative;
    width: 90vw;
    margin: 20vw auto;
  }
  .app {
    position: relative;
    width: 80vw;
    height: 60vh;
    margin: 0 auto;
    overflow: hidden;
  }

  button {
    width: 5vw;
    height: 5vw;
    font-size: 3vw;
    color: #fff;
    border: none;
    border-radius:1vw;
    background-color: rgba(0,0,0,0.2);
  }

  button:hover {
    background-color: rgba(0,0,0,0.8);
  }

  .leftArrow {
    position: absolute;
    top: 15vh;
    left: 0px;
    z-index: 5;
  }

  .rightArrow {
    position: absolute;
    top: 15vh;
    left: 85vw;
    z-index: 5;
  }

  .container {
    position: absolute;
    top: 0;
    left: 0px;
    width: 500vw;
    display: flex;
    flex-wrap: nowrap;
    align-items: center;
  }

  .transform {
    transition: 2000ms ease 0s;
  }

@media screen and (min-width: 1200px) {
  .image {
    width: 20vw;
  }

  img {
    width: 20vw;
  }
}

@media screen and (min-width: 600px) and (max-width: 1200px) {
  .image {
    width: 40vw;
    font-size: 10vh;
  }

  img {
    width: 40vw;
  }
}

@media screen and (max-width: 600px) {
  .image {
    width: 80vw;
    font-size: 10vh;
  }

  img {
    width: 80vw;
  }
}

</style>
