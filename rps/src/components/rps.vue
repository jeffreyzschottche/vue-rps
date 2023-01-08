<template>
    <h2>{{ title }} </h2>
    <h5>Choose wisely young anakin
    </h5>
    <h6>We will play a game until one score hits 5</h6>
    <div>
        <button v-on:click="play('rock')">Rock</button>
        <button v-on:click="play('paper')">Paper</button>
        <button v-on:click="play('scissors')">Scissors</button>
    </div>

    <div>Player chose: {{ playerChoice }}</div>
    <div>Computer chose: {{ computerChoice }}</div>

    <div> <b> Player Score: {{ scorePlayer }} </b></div>
    <div> <b> Computer Score: {{ scorePC }} </b></div>
    <div> <b> Draws: {{ tie }} </b></div>
    <div>
        <h1>{{ winner }}</h1>
    </div>

    <h4 v-if="newGameBool">Want to start a new game?</h4>
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
</style>