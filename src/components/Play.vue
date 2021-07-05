<template>
<div class="container">
  <div class="row">
    <div class="col row between">
      <div class="square" :class="squares[0].color" v-on:click="onClickSquare(0)"></div>
      <div class="square" :class="squares[1].color" v-on:click="onClickSquare(1)"></div>
    </div>
  </div>

  <div class="row">
    <div class="col row center">
      <div class="square" :class="squares[2].color" v-on:click="onClickSquare(2)"></div>
    </div>
  </div>

  <div class="row">
    <div class="col row between">
      <div class="square" :class="squares[3].color" v-on:click="onClickSquare(3)"></div>
      <div class="square" :class="squares[4].color" v-on:click="onClickSquare(4)"></div>
    </div>
  </div>

  <button class="btn" v-on:click="startGame">PLAY GAME</button>
</div>
</template>

<script>
export default {
  name: 'Play',
  data() {
    return {
      squares: [
        {
          id: 0,
          color : 'green'
        },
        {
          id: 1,
          color : 'red'
        },
        {
          id: 2,
          color : 'purple'
        },
        {
          id: 3,
          color : 'orange'
        },
        {
          id: 4,
          color : 'blue'
        }
      ]
    }
  },
  methods: {
    startGame(){
      this.squares.sort(() => Math.random() - 0.5);
    },
    onClickSquare(){
      
    }
  },
}
</script>

<style scoped>
@import 'styles.css';
</style>
