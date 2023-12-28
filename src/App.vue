<template>
  <the-header></the-header>
      <base-dialog v-if="firstTime">
        <template #header>
          <h2>Welcome!</h2>
        </template>
        <template #message>
          <label>Please enter your name:</label>
          <input type="text" name="name" id="name" @change="getPlayerName"/>
          <p class="dialog-message" v-if="invalidName">Please enter a name.</p>
        </template>
        <template #buttons>
          <base-button @click="confirmPlayerName">Confirm</base-button>
        </template>
      </base-dialog>
      <base-dialog v-if="overallWinner">
          <template #header>
            <h2>Winner!</h2>
          </template>
          <template #message>
            <p>{{ overallWinner }} wins!</p>
          </template>
          <template #buttons>
            <base-button @click="resetGame">Play Again</base-button>
          </template>
        </base-dialog>
  <div id="gameboard">
    <player-card @select-rock="selectRock" @select-paper="selectPaper" @select-scissors="selectScissors"></player-card>
    <div id="battle-display">
      <player-image :selectedObject="selectedObject"></player-image>
      <h2>Vs</h2>
      <computer-image :computerObject="computerObject"></computer-image>
      <base-button id="fight-button" @click="getComputerObject">Fight!</base-button>
    </div>
  </div>
  <div id="result">
    <p v-if="playerWins">Player Wins!</p>
    <p v-if="computerWins">Computer Wins!</p>
    <p v-if="draw">Its a Draw!</p>
    <p v-if="overallWinner">The winner is {{ overallWinner }}</p>
  </div>
  <the-scoreboard :playerName="playerName" :playerScore="playerScore" :computerScore="computerScore "></the-scoreboard>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import PlayerCard from './components/PlayerCard.vue';
import PlayerImage from './components/PlayerImage.vue';
import ComputerImage from './components/ComputerImage.vue';
import BaseButton from './components/UI/BaseButton.vue';
import TheScoreboard from './components/TheScoreboard.vue';

export default {
  components: {
    TheHeader,
    PlayerCard,
    PlayerImage,
    ComputerImage,
    BaseButton,
    TheScoreboard
  },
  data() {
    return {
      selectedObject: {
        name: 'paper',
        source: 'src/assets/paper.png'
      },
      computerObject: {
        name: '',
        source: 'src/assets/question.png'
      },
      rock: {
        name: 'rock',
        source: 'src/assets/rock.png'
      },
      paper: {
        name: 'paper',
        source: 'src/assets/paper.png'
      },
      scissors: {
        name: 'scissors',
        source: 'src/assets/scissors.png'
      },
      playerWins: false,
      computerWins: false,
      draw: false,
      playerScore: 0,
      computerScore: 0,
      overallWinner: '',
      playerName: '',
      firstTime: true
    }
  },
  methods: {
    selectRock(){
      this.selectedObject = this.rock;
    },
    selectPaper(){
      this.selectedObject = this.paper;
    },
    selectScissors(){
      this.selectedObject = this.scissors;
    },
    confirmName(name){
      this.playerName = name;
    },
    getPlayerName(event) {
      this.playerName = event.target.value;
    },
    confirmPlayerName() {
      if (this.playerName.trim() === '') {
        this.invalidName = true;
      }

      this.firstTime = false;

    },
    getComputerObject(){
      const randomNumber = Math.floor(Math.random() * 4);

      this.playerWins = false;
      this.computerWins = false;
      this.draw = false;


      if( randomNumber === 1){
        this.computerObject = this.rock;
      }else if (randomNumber === 2){
        this.computerObject = this.paper;
      }else if (randomNumber ===3){
        this.computerObject = this.scissors;
      }

      if (this.computerObject === this.rock && this.selectedObject === this.rock){
        console.log("Its a draw!")
        this.draw = true;
      } else if (this.computerObject === this.rock && this.selectedObject === this.scissors){
        console.log("Computer wins!")
        this.computerWins = true;
        this.computerScore++;
      } else if (this.computerObject === this.rock && this.selectedObject === this.paper){
        console.log("Player wins!")
        this.playerScore++;
        this.playerWins = true;
      } else if (this.computerObject === this.paper && this.selectedObject === this.paper) {
        console.log("Its a draw!")
        this.draw = true;
      } else if (this.computerObject === this.paper && this.selectedObject === this.scissors) {
        console.log("Player wins!")
        this.playerScore++;
        this.playerWins = true;
      } else if (this.computerObject === this.paper && this.selectedObject === this.rock) {
        console.log("Computer wins!")
        this.computerWins = true;
        this.computerScore++;
      } else if (this.computerObject === this.scissors && this.selectedObject === this.paper) {
        console.log("Computer wins!")
        this.computerScore++;
        this.computerWins = true;
      } else if (this.computerObject === this.scissors && this.selectedObject === this.scissors) {
        console.log("Its a draw!")
        this.draw = true;
      } else if (this.computerObject === this.scissors && this.selectedObject === this.rock) {
        console.log("Player wins!")
        this.playerWins = true;
        this.playerScore++;
      }

      if(this.computerScore === 5){
        this.overallWinner = 'Computer';
      } else if (this.playerScore === 5){
        this.overallWinner = 'Player'
      }
    },
    resetGame(){
      this.playerWins = false,
      this.computerWins = false,
      this.draw = false,
      this.playerScore = 0,
      this.computerScore = 0,
      this.overallWinner = '',
      this.firstTime = true
    }
  }
}
</script>



<style >

@import url('https://fonts.googleapis.com/css2?family=Roboto:wght@400;700&display=swap');

body {
  font-family: 'Roboto', sans-serif;
  background-color: rgb(211, 211, 224);
  width: 100%;
}

#app {
  width: 100%;
}

#gameboard {
  display: flex;
  margin-top: 8rem;
}

#battle-display {
  display: flex;
  gap: 2rem;
  padding-top: 4.5rem
}

#fight-button {
  margin-left: 5rem;
  margin-top: 1rem;
}

#result {
  width: 50%;
  margin: 4rem auto;
}

p {
  display: block;
  text-align: center;
  font-size: 2rem;
}

</style>
