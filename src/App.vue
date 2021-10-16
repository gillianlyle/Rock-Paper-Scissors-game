<template>
  <div class="wrapper">
    <header class="header">
      <h1 class="h1">
        <img src="./assets/images/logo.svg">
      </h1>
      <div class="score">
        <h2 class="score__title">
          Score
        </h2>
        <p class="score__count">
          {{ count }}
        </p>
      </div>
    </header>

    <main class="main">
      <div
        v-if="!playerGuess"
        class="player"
      >
        <button
          class="btn__Rock"
          aria-label="Rock"
          @click="getPlayerGuess('Rock')"
        />
        <button
          class="btn__Paper"
          aria-label="Paper"
          @click="getPlayerGuess('Paper')"
        />
        <button
          class="btn__Scissors"
          aria-label="Scissors"
          @click="getPlayerGuess('Scissors')"
        />
      </div>
      <div
        v-if="playerGuess"
        class="computer"
      >
        <div class="guess">
          <p class="player__guess">
            You picked
          </p>
          <div :class="`btn__${playerGuess}`" />
        </div>
          
        <div class="confirm-winner">
          <p> {{ winner }} </p>
          <button
            class="btn btn--white"
            @click="playAgain()"
          >
            Play again
          </button>
        </div>

        <div class="guess">
          <p class="computer__guess">
            The house picked
          </p>
          <div :class="`btn__${computerGuess}`" />
        </div>
      </div>
    </main>

    <footer class="footer">
      <button
        id="show-modal"
        class="btn"
        @click="showModal = true"
      >
        Rules
      </button>
    </footer>

    <transition name="modal">
      <modal
        v-if="showModal"
        @close="showModal = false"
      >
        <template #header>
          <h2 class="h2">
            Rules
          </h2>
        </template>

        <template #body>
          <img src="../src/assets/images/image-rules.svg">
        </template>
      </modal>
    </transition>
  </div>
</template>

<script>
import Modal from './components/Modal.vue';

 export default {
   name: 'App',
   components:{
     Modal
    },
   data(){
     return {
       count: 0,
       playerGuess: '',
       computerGuess: '',
       winner: '',
       showModal: false,
     }
   },
   watch:{
     playerGuess(){
       if(this.playerGuess !== ''){
        this.getWinner();
        this.getScore();
       }
      },
   },
   created(){
     this.getComputerGuess();
   },
   methods: {
      getComputerGuess(){
       let number = Math.random();

       if (number < 0.25) {
         return this.computerGuess = 'Rock'
       }

       if (number = 0.25 && number < 0.65){
         return this.computerGuess = 'Paper'
       }

       return this.computerGuess = 'Scissors'
     },
     getPlayerGuess(guess){       
       if (guess === 'Rock'){
         return this.playerGuess = 'Rock'
       }

        if (guess === 'Paper'){
          return this.playerGuess = 'Paper'
        }

       return this.playerGuess = 'Scissors'
     },
     getWinner(){

        if ( this.playerGuess === 'Paper' && this.computerGuess === 'Rock'){
          return this.winner = 'YOU WIN'
        }

        if ( this.playerGuess === 'Rock' && this.computerGuess === 'Scissors'){
          return this.winner = 'YOU WIN'
        }

        if ( this.playerGuess === 'Scissors' && this.computerGuess === 'Paper'){
          return this.winner = 'YOU WIN'
        }

        if ( this.playerGuess ===  this.computerGuess){
          return this.winner = "IT'S A DRAW"
        }

        return this.winner = 'YOU LOSE';
      },
      getScore(){
        if (this.winner === 'YOU WIN'){
          return this.count += 1;
        }

        if (this.winner === "IT'S A DRAW"){
          return this.count;
        }

        return this.count -= 1;
      },
      playAgain(){
        this.playerGuess = '';
        this.getComputerGuess();
        this.winner = '';
      }
   }
 }
</script>


