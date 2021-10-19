<template>
  <div class="app">
    <div class="leftArrow" @click="leftMove"><button> 《 </button></div>
    <div class="container" :style="{left: state.imgLeft + 'px'}">
      <div  class="image" v-for="(item, index) in state.list" :key="index">
        <img :src="require('@/assets/' + item)" />
      </div>
    </div>
    <div class="rightArrow" @click="rightMove()"><button> 》 </button></div>
    <div class="dots">
      <div class="dot" :class="{active: index === state.currentPage}" v-for="(item, index) in state.list" :key="index">
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { reactive } from 'vue'
export default {
  name: 'App',
  setup () {
    const state = reactive({
      list: ['1.png', '2.png', '3.png'],
      imgLeft: 0,
      timeval: 1,
      currentPage: 0
    })

    function leftMove () {
      let moveDist = 0
      if (state.imgLeft <= -800 * (state.list.length - 1)) {
        state.imgLeft = -800 * (state.list.length - 1)
      } else {
        setInterval(() => {
          if (moveDist <= -800) {
            clearInterval()
          } else {
            moveDist -= Math.round(8 / state.timeval)
            state.imgLeft -= Math.round(8 / state.timeval)
          }
        }, 10)
        state.currentPage++
      }
    }

    function rightMove () {
      let moveDist = 0
      if (state.imgLeft >= 0) {
        state.imgLeft = 0
      } else {
        setInterval(() => {
          if (moveDist >= 800) {
            clearInterval()
          } else {
            moveDist += Math.round(8 / state.timeval)
            state.imgLeft += Math.round(8 / state.timeval)
          }
        }, 10)
        state.currentPage--
      }
    }

    return {
      state,
      leftMove,
      rightMove
    }
  }
}
</script>

<style>
.app {
  position: relative;
  width: 800px;
  height: 600px;
  margin: 200px auto;
  overflow: hidden;
}

button {
  width: 50px;
  height: 100px;
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
  top: 242px;
  left: 0px;
  z-index: 5;
}

.rightArrow {
  position: absolute;
  top: 242px;
  left: 750px;
  z-index: 5;
}

.container {
  position: absolute;
  top: 0;
  left: 0px;
  width: 2400px;
  display: flex;
  flex-wrap: nowrap;
}

.image {
  width: 800px;
  /* height: 600px; */
  font-size: 100px;
}

img {
  width: 800px;
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
