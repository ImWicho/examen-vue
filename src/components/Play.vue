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
          color : 'green',
          active: false,
          position: undefined
        },
        {
          color : 'red',
          active: false,
          position: undefined
        },
        {
          color : 'purple',
          active: false,
          position: undefined
        },
        {
          color : 'orange',
          active: false,
          position: undefined
        },
        {
          color : 'blue',
          active: false,
          position: undefined
        }
      ],
      positions: [0,1,2,3,4],
      isStarted: false
    }
  },
  methods: {
    async startGame(){
      this.positions.sort(() => Math.random() - 0.5);

      for(let i = 0; this.squares.length > i; i++){
        this.squares[this.positions[i]].active = true;
        this.squares[this.positions[i]].position = this.positions[i];
        await this.sleep(2000);
        this.squares[this.positions[i]].active = false;
        await this.sleep(2000);
      }

      // setTimeout(() => {
      //   this.squares[this.positions[0]].active = true;
      //   this.squares[this.positions[0]].position = this.positions[0];
      //   setTimeout(() => {
      //     this.squares[this.positions[0]].active = false;
      //   },2000);
      // },2000);

      // setTimeout(() => {
      //   this.squares[this.positions[1]].active = true;
      //   this.squares[this.positions[1]].position = this.positions[1];
      //     setTimeout(() => {
      //     this.squares[this.positions[1]].active = false;
      //   },2000);
      // },4000);

      // setTimeout(() => {
      //   this.squares[this.positions[2]].active = true;
      //   this.squares[this.positions[2]].position = this.positions[2];
      //   setTimeout(() => {
      //     this.squares[this.positions[2]].active = false;
      //   },2000);
      // },6000);

      // setTimeout(() => {
      //   this.squares[this.positions[3]].active = true;
      //   this.squares[this.positions[3]].position = this.positions[3];
      //   setTimeout(() => {
      //     this.squares[this.positions[3]].active = false;
      //   },2000);
      // },8000);

      // setTimeout(() => {
      //   this.squares[this.positions[4]].active = true;
      //   this.squares[this.positions[4]].position = this.positions[4];
      //   setTimeout(() => {
      //     this.squares[this.positions[4]].active = false;
      //   },2000);
      // },10000);

      
    },
    onClickSquare(idx){
      if(this.squares[idx].position === this.positions[0]){
        this.positions.splice(0, 1);
        this.squares[idx].active = true;
      }else{
        alert('Has perdido!');
        this.resetGame();
      }
    },
    resetGame(){
      this.squares.forEach((x) => {
        x.active = false;
        x.position = undefined;
      });
      this.isStarted = false;
    },
    sleep(ms){
      return new Promise(resolve => setTimeout(resolve,ms))
    }
  },
}
</script>

<style scoped>
@import 'styles.css';
</style>
