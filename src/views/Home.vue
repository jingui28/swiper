<template>
  <div class="home">
    <div class="leftArrow" @mouseleave="transform" @click="leftMove"><button> 《 </button></div>
    <div class="app">
      <div class="container" :class="{transform: state.transform}" :style="{left: state.imgLeft + 'px'}">
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
      list: ['1.jpg', '2.jpg', '3.jpg', '4.jpg', '5.jpg', '6.jpg', '7.jpg', '8.jpg', '9.jpg', '10.jpg', '11.jpg', '12.jpg', '13.jpg', '14.jpg', '15.jpg', '16.jpg', '1.jpg', '2.jpg', '3.jpg', '4.jpg', '5.jpg'],
      imgLeft: 0,
      timeval: 1,
      currentPage: 0,
      transform: true
    })

    var timer = setInterval(func, 2000)
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
      state.imgLeft = -800 * state.currentPage
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
      timer = setInterval(func, 2000)
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
  width: 900px;
  margin: 200px auto;
}
.app {
  position: relative;
  width: 800px;
  height: 200px;
  margin: 0 auto;
  overflow: hidden;
}

button {
  width: 50px;
  height: 50px;
  font-size: 30px;
  color: #fff;
  border: none;
  border-radius: 5px;
  background-color: rgba(0,0,0,0.2);
}

button:hover {
  background-color: rgba(0,0,0,0.8);
}

.leftArrow {
  position: absolute;
  top: 75px;
  left: 0px;
  z-index: 5;
}

.rightArrow {
  position: absolute;
  top: 75px;
  left: 850px;
  z-index: 5;
}

.container {
  position: absolute;
  top: 0;
  left: 0px;
  width: 3600px;
  display: flex;
  flex-wrap: nowrap;
  align-items: center;
  /* transform: translateX(-200px); */
  /* transition: 2000ms ease 0s; */
}

.transform {
  transition: 2000ms ease 0s;
}

.image {
  width: 200px;
  /* height: 600px; */
  font-size: 100px;
}

img {
  width: 200px;
}

.dots {
  position: absolute;
  bottom: 20px;
  right: 50px;
}

.dot {
  float: left;
  width: 20px;
  height: 20px;
  line-height: 20px;
  text-align: center;
  border-radius: 50%;
  background: #aaa;
  margin-right: 10px;
}

.active {
  background: red;
}
</style>
