<template>
<div class="box">
  <div class="content">
    <h2 class="has-text-weight-bold" style="margin-bottom: 30px;">{{ question }}</h2>
    <div class="columns is-multiline is-centered">
      <div class="column is-half">
        <button class="button is-link is-large" @click="onAnswer(btnData[0].correct)">{{ btnData[0].answer }}</button>
      </div>
      <div class="column is-half">
        <button class="button is-link is-large" @click="onAnswer(btnData[1].correct)">{{ btnData[1].answer }}</button>
      </div>
      <div class="column is-half">
        <button class="button is-link is-large" @click="onAnswer(btnData[2].correct)">{{ btnData[2].answer }}</button>
      </div>
      <div class="column is-half">
        <button class="button is-link is-large" @click="onAnswer(btnData[3].correct)">{{ btnData[3].answer }}</button>
      </div>
    </div>
  </div>
</div>
</template>
<script>
const MODE_ADDITION = 1;
const MODE_SUBTRACTION = 2;
export default {
  data() {
    return {
      question: 'Oops, an error ocurred :/',
      btnData: [
        {correct: true, answer: 0},
        {correct: false, answer: 0},
        {correct: false, answer: 0},
        {correct: false, answer: 0}
      ]
    };
  },
  methods: {
    generateQuestion() {
      const firstNumber = this.generateRandomNumber(1, 100);
      const secondNumber = this.generateRandomNumber(1, 100);
      const modeNumber = this.generateRandomNumber(1, 2);

      let correctAnswer = 0;

      switch (modeNumber) {
        case MODE_ADDITION:
          correctAnswer = firstNumber + secondNumber;
          this.question = `What's ${firstNumber} + ${secondNumber}?`;
          break;
        case MODE_SUBTRACTION:
          correctAnswer = firstNumber - secondNumber;
          this.question = `What's ${firstNumber} - ${secondNumber}?`;
          break;
        default:
          correctAnswer = 0;
          this.question = 'Oops, an Error occurred :/';
      }
      // Generate the random answers for the four buttons. All will initially be a random number from the correct number plus and minus 10.
      // For example - if the correct answer is 10, the buttons will generate random answers from 0 - 30.
      this.btnData[0].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
      this.btnData[0].correct = false;
      this.btnData[1].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
      this.btnData[1].correct = false;
      this.btnData[2].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
      this.btnData[2].correct = false;
      this.btnData[3].answer = this.generateRandomNumber(correctAnswer - 10, correctAnswer + 10, correctAnswer);
      this.btnData[3].correct = false;
      // Setting one of the four buttons to the correct answer; changing 'correctAnswer' to true and the 'answer' to the correct one.
      const correctButton = this.generateRandomNumber(0, 3);
      this.btnData[correctButton].correct = true;
      this.btnData[correctButton].answer = correctAnswer;
    },
    generateRandomNumber(min, max, except) {
      // The returned value is no lower than (and may possibly equal) min, and is less than (and not equal) max
      const rndNumber = Math.round(Math.random() * (max - min)) + min;
      console.log(min, max, rndNumber);
      // Prevents the correct answers being called.
      if (rndNumber == except) {
        return this.generateRandomNumber(min, max, except);
      }
      return rndNumber;
    },
    onAnswer(isCorrect) {
      this.$emit('answered', isCorrect);
    }
  },
  created() {
    this.generateQuestion();
  }
}
</script>
<style>

</style>
