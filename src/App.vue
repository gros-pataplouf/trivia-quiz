<template>
  <v-app>
    <v-main>
      <QuizHeader :correctGuesses="correctGuesses" :totalGuesses="totalGuesses"/>
      <QuestionBox v-if="questions.length" :currentQuestion="questions[counter]" :increment="increment" :updateScores="updateScores"/>
    </v-main>
  </v-app>
</template>

<script>
import QuizHeader from './components/QuizHeader';
import QuestionBox from './components/QuestionBox';

export default {
  name: 'App',

  components: {
    QuizHeader,
    QuestionBox,
  },
  mounted: function() {
    console.log(this.currentQuestion)
    fetch('https://opentdb.com/api.php?amount=10&category=22&type=multiple', {
      method: 'get'
    })
    .then(response => response.json())
    .then(jsonData => this.questions = jsonData.results)
    .catch(e => console.error(e))

  },

  data: () => ({
    questions: [],
    counter: 0,
    currentQuestion: {},
    correctGuesses: 0,
    totalGuesses: 0
 
  }),
  methods: {
    increment() {
      this.counter++;
    },
    updateScores(correctGuess) {
      if (correctGuess) {
        this.correctGuesses++;
      }
      this.totalGuesses++;
    }
  }
};
</script>
