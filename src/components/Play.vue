<template>
<div class="container">
  <div class="row">
    <div class="col row between">
      <div class="square" :class="squares[0].active ? squares[0].color : ''" v-on:click="onClickSquare(0)"></div>
      <div class="square" :class="squares[1].active ? squares[1].color : ''" v-on:click="onClickSquare(1)"></div>
    </div>
  </div>

  <div class="row">
    <div class="col row center">
      <div class="square" :class="squares[2].active ? squares[2].color : ''" v-on:click="onClickSquare(2)"></div>
    </div>
  </div>

  <div class="row">
    <div class="col row between">
      <div class="square" :class="squares[3].active ? squares[3].color : ''" v-on:click="onClickSquare(3)"></div>
      <div class="square" :class="squares[4].active ? squares[4].color : ''" v-on:click="onClickSquare(4)"></div>
    </div>
  </div>

  <button class="btn" :disabled="isLoading" v-on:click="startGame">PLAY GAME</button>
</div>
</template>

<script>
const sound = require("@/assets/erro.mp3");
const init = require("@/assets/noti.mp3");
export default {
  name: 'Play',
  data() {
    return {
      squares: [
        {
          color : 'green',
          active: false,
          position: undefined,
          clicked : false
        },
        {
          color : 'red',
          active: false,
          position: undefined,
          clicked : false
        },
        {
          color : 'purple',
          active: false,
          position: undefined,
          clicked : false
        },
        {
          color : 'orange',
          active: false,
          position: undefined,
          clicked : false
        },
        {
          color : 'blue',
          active: false,
          position: undefined,
          clicked : false
        }
      ],
      positions: [0,1,2,3,4],
      isLoading: false
    }
  },
  methods: {
    async startGame(){
      this.positions.sort(() => Math.random() - 0.5);
      this.isLoading = true;
      for(let i = 0; this.squares.length > i; i++){
        await this.sleep(2000);
        this.play(init);
        this.squares[this.positions[i]].active = true;
        this.squares[this.positions[i]].position = this.positions[i];
        await this.sleep(2000);
        this.squares[this.positions[i]].active = false;
      }
      this.isLoading = false;      
    },
    onClickSquare(idx){
      if(this.isLoading || this.squares[idx].clicked){ return; }
      if(this.squares[idx].position === this.positions[0]){
        this.positions.splice(0, 1);
        this.squares[idx].active = true;
        this.squares[idx].clicked = true;
      }else{
        this.play(sound);
        alert('Has perdido!');
        this.resetGame();
      }

      if(this.positions.length === 0){
        alert('Has ganadoooooooooooooooo');
        this.resetGame();
      }
    },
    resetGame(){
      this.squares.forEach((x) => {
        x.active = false;
        x.position = undefined;
        x.clicked = false;
      });
      this.isStarted = false;
    },
    sleep(ms){
      return new Promise(resolve => setTimeout(resolve,ms))
    },
    play(x) {
      const audio = new Audio(x);
      audio.play();
  }
  },
}
</script>

<style scoped>
@import 'styles.css';
</style>
