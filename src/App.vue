<template>
  <div id="app">
    <div class="board">
      <div 
        class="grid" 
        v-for='(grid,id) in grids' 
        :key='id'
        @click='setGrid(id)'>
        {{setSymbol(grid)}}
      </div>
    </div>
    <div class="info">
      <p>Player: {{setSymbol(player)}}</p>
      <p>Winner: {{setSymbol(winner)}}</p>
      <button @click='reset'>reset</button>
    </div>
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
const lines = [
  [0,1,2],[3,4,5],[6,7,8],
  [0,3,6],[1,4,7],[2,5,8],
  [0,4,8],[2,4,6]
]

export default {
  data () {
    return {
      player: 1,
      grids: [
        0,0,0,
        0,0,0,
        0,0,0
      ]
    }
  },
  computed:{
    winner(){
    //lines[i]解構為[a,b,c]
    // return lines.reduce((winner,[a,b,c]) => {
    //   if(winner !== 0) return winner
    //   const sum = this.grids[a] + this.grids[b] + this.grids[c] 
    //   if(sum === 3) return 1
    //   if(sum === -3) return -1
    //   return 0
    // },0)


    for(let i = 0; i < 8; i++){
      const [a,b,c] = lines[i] //解構
      const sum = this.grids[a] + this.grids[b] + this.grids[c] 
      if(sum === 3) return 1
      if(sum === -3) return -1
    }
    return 0
    },
  },
  methods:{
    setGrid(id){
      if(this.grids[id] !== 0) return
      if(this.winner !== 0) return


      this.$set(this.grids, id ,this.player)
      this.player = -this.player
    },
    setSymbol(num){
      return num === 0 ? '' : num === -1 ? 'X' :'O'
    },
    reset(){
      this.player = 1,
      this.grids = [
        0,0,0,
        0,0,0,
        0,0,0
      ]
    }
  }
}
</script>

<style>
.board{
  display: flex;
  flex-flow: row wrap;
  width: 400px;
  height: 400px;
  align-content: flex-start;
  /* justify-content:space-between; */
  margin: 0 auto
  }
.grid{
  width: 33%;
  height: 33%;
  box-sizing: border-box;
  border: 1px solid gray;
  text-align: center;
  font-size: 50px;
  cursor: pointer;
  line-height: 130px;
}
.info{
  font-size: 40px;
}
</style>
