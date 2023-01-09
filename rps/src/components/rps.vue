<template>
    <link
  rel="stylesheet"
  href="https://unpkg.com/98.css">
  <div class="window" >
    <div class="title-bar">
      <div class="title-bar-text"><h2>{{ title }} </h2></div>
      <div class="title-bar-controls">
        <button aria-label="Minimize"></button>
        <button aria-label="Maximize"></button>
        <button aria-label="Close"></button>
      </div>
    </div>
    <div class="window-body">
        <h4>Choose wisely young anakin
        </h4>
        <h4>We will play a game until one of the player's score hits 5</h4>
    </div>
  </div>

    <div class="choices">
        <button v-on:click="play('rock')">Rock</button>
        <button v-on:click="play('paper')">Paper</button>
        <button v-on:click="play('scissors')">Scissors</button>
    </div>
    <ul class="tree-view">
        <div>Player choice: {{ playerChoice }}</div>
        <div>Computer choice: {{ computerChoice }}</div>
        
        <strong style="color: purple">✨ Draws : {{ tie }} ✨</strong>
        <strong style="color: blue">✨ Player Score : {{ scorePlayer }} ✨</strong>
        <strong style="color: blue">✨ Computer Score : {{ scorePC }} ✨</strong>

      </ul>


      <div class="title-bar-text"><h3>{{ winner }} </h3></div>
      <div class="title-bar-text"><h4 v-if="newGameBool">Want to start a new game?</h4></div>
      <button v-if="newGameBool" v-on:click="resetGame()">New Game</button>
</template>

<script>
    export default {
        name: 'RPS',
        data() {
            return {
                playerChoice: '',
                computerChoice: '',
                outcome: '',
                scorePlayer: 0,
                scorePC: 0,
                tie: 0,
                winner: '',
                newGameBool: false,
            }
        },
        props: {
            title: String,
        },
        methods: {
            
            newGame(){
                this.newGameBool = true;
            },
            resetGame(){
                this.playerChoice = '',
                this.computerChoice = '',
                this.outcome = '',
                this.scorePlayer = 0,
                this.scorePC = 0,
                this.tie = 0,
                this.winner = '',
                this.newGameBool = false
            },

            calculateWinner(player, computer) {
                if (player === computer) {
                    
                    this.tie++;
                    return;
                } else if (player === 'rock' && computer === 'scissors' ||
                    player === 'scissors' && computer === 'paper' ||
                    player === 'paper' && computer === 'rock') {
                        if(this.scorePlayer < 4){
                            this.scorePlayer++;
                        }
                        else if(this.scorePlayer === 4){
                            this.scorePlayer++;
                            this.winner = 'The winner of the game is player';
                            this.newGame();
                        }
                  
                } else {
                    if(this.scorePC < 4){
                        this.scorePC++;
                    }else if(this.scorePC === 4){
                        this.scorePC++;
                        this.winner = "The winner of the game is the pc";
                        this.newGame();
                    }
                }
            },
            play(option) {
                // logic for handling the play goes here
                this.playerChoice = option;
                this.computerChoice = this.computerChoiceRandomized();
                this.calculateWinner(this.playerChoice, this.computerChoice);
            },
            computerChoiceRandomized() {
                // This will make the computer choose itself
                const randomNum = Math.floor(Math.random() * 3);
                if (randomNum == 1) {
                    return 'rock'
                } else if (randomNum == 2) {
                    return 'paper'
                } else {
                    return 'scissors'
                }
            }
        }
    }
</script>

<style>
.choices button{
    margin: 1em;
}
body{
    background-image: url("https://upload.wikimedia.org/wikipedia/en/2/27/Bliss_%28Windows_XP%29.png");
    background-size: cover;
    background-repeat: no-repeat;
}
</style>