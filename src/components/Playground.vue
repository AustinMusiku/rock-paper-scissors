<template>
  <div class="playground">
    <div class="console">
      <div class="you">
        <h2>You</h2>
        <p class="consoleScore">{{youScore}}</p>
      </div>
      <div class="browser">
        <h2>Browser</h2>
        <p class="consoleScore">{{browserScore}}</p>
      </div>
    </div>
    <div class="controls">
      <div class="control" v-for="option in options" @click="youChoose(option)">
        <i>{{option.symbol}}</i>
        <p>{{option.name}}</p>
      </div>
    </div>
    <div v-if="totalscore==5" class="comment">

    </div>
  </div>
</template>

<script>
export default {
  name: 'Playground',
  props: ['gameOver'],
  data(){
    return{
      youScore: 0,
      browserScore: 0,
      totalScore: 0,
      scoreComment:'',
      youOption: null,
      browserOption: null,
      options: [
        { symbol: '✊', name: 'rock', beats: 'scissors' },
        { symbol: '✋', name: 'paper', beats: 'rock' },
        { symbol: '✌', name: 'scissors', beats: 'paper' }
      ]
    }
  },
  methods: {
    browserChoose(){
      this.browserOption = this.options[Math.floor(Math.random()*3)];
      console.log(this.browserOption);
      this.evaluate();
    },

    // evaluate choices and assign score
    evaluate(){
      if(this.browserOption.name==this.youOption.beats){
          this.youScore++;
      }else if(this.youOption.name==this.browserOption.beats){
          this.browserScore++;
      }else{
        this.youScore;
      }
      this.totalScore=this.youScore + this.browserScore;
      this.endGame()
    },

    // End the round once winner is found
    endGame(){
      if(this.totalScore>=5){
        
        setTimeout(() => {
          if(this.youScore > this.browserScore){
            this.scoreComment='You Win!';
          }else{
            this.scoreComment='You Loose!';
          }
          this.$emit('endGame', this.scoreComment);
        }, 250);
      }else{
        console.log(this.totalScore);
      }
    },
    youChoose(option){
      this.youOption = option;
      this.browserChoose();
    }
  }
}
</script>

<style>
.playground{
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  max-width: 600px;
  height: 300px;
}
.console,
.controls{
  display: flex;
  flex-direction: row;
  justify-content: space-around;
  align-items: center;
  height: 100%;
}
.consoleScore{
  margin: 0;
  font-size: 64px;
}
.controls{
  padding: 4em 0;
}
.control{
  display: flex;
  flex-direction: column;
  gap: .25em;
  cursor: pointer;
}
i{
  font-size: 50px;
}
</style>