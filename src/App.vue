<template>
  <section class="section">
    <div class="container is-fluid">
      <div class="columns is-mobile has-text-centered">
        <div class="column is-two-thirds is-offset-one-fifth">
          <div class="content">
            <h1 class="has-text-weight-bold">Maths Quiz</h1>
          </div>
        </div>
      </div>
      <div class="columns is-mobile has-text-centered">
        <div class="column is-two-thirds is-offset-one-fifth">
          <div class="content">
            <transition name="flip" mode="out-in">
              <component :is="mode" @answered="answered($event)" @confirmed="mode = 'app-question'"></component>
            </transition>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>

import Answer from './components/Answer.vue';
import Question from './components/Question.vue';

export default {
  data(){
    return{
      mode: 'app-question'
    }
  },
  methods: {
    answered(isCorrect){
      if(isCorrect){
        this.mode = 'app-answer';
      } else {
          this.mode = 'app-question';
          alert("Sorry, that's the wrong answer, try again.");
      }
    }
  },
  components: {
    appQuestion: Question,
    appAnswer: Answer
  }
}
</script>

<style>
.flip-enter{
  /* transform: rotateY(0deg); */
}

.flip-enter-active{
  /* Forwards = Stays at the final state */
  animation: flip-in 0.3s ease-out forwards;
}

.flip-leave{
  /* transform: rotateY(0deg); */
}

.flip-leave-active{
  animation: flip-out 0.3s ease-out forwards;
}

@keyframes flip-out{
  from{
    transform: rotateY(0deg);
  }
  to{
    transform: rotateY(90deg);
  }
}

@keyframes flip-in{
  from{
    transform: rotateY(90deg);
  }
  to{
    transform: rotateY(0deg)
  }
}
</style>
