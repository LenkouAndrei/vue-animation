<template>
  <div class="container">
    <h1 class="text-center">The Super Quiz</h1>
    <div class="row">
      <div class="col-xs-8 col-xs-offset-2">
        <select v-model="alertAnimation" class="form-control margin-bottom">
          <option value="fade">Fade</option>
          <option value="slide">Slide</option>
        </select>
      </div>
    </div>
    <div class="row">
      <div class="col-xs-8 col-xs-offset-2">
        <transition :name="alertAnimation" appear mode="out-in">
          <app-questions v-if="!answerRight && !answerError" :current="currentOption" key="question"></app-questions>
          <app-right-answer v-if="answerRight" key="right"></app-right-answer>
          <app-wrong-answer v-if="answerError" key="wrong"></app-wrong-answer>
        </transition>
      </div>
    </div>
  </div>
</template>

<script>
  import Questions from './components/Questions.vue';
  import RightAnswer from './components/RightAnswer.vue';
  import WrongAnswer from './components/WrongAnswer.vue';
  import { eventBus } from './main';

  export default {
    components: {
      appQuestions: Questions,
      appRightAnswer: RightAnswer,
      appWrongAnswer: WrongAnswer
    },
    data() {
      return {
        answerError: false,
        answerRight: false,
        currentOption: 0,
        alertAnimation: 'slide'
      }
    },
    created() {
        eventBus.$on('switchRight', () => {
            this.answerRight = true
        });
        eventBus.$on('switchError', () => {
            this.answerError = true
        });
        eventBus.$on('next', () => {
              this.answerRight = false
              this.currentOption++
        });
        eventBus.$on('stay', () => {
            this.answerError = false
        });
    }
  }
</script>

<style lang="scss">
.margin-bottom {
  margin-bottom: 20px;
}
.slide-enter {
  opacity: 0;
}
.slide-enter-active {
  animation: slide-in .5s ease-out forwards;
  transition: opacity .5s;
}
.slide-leave {

}
.slide-leave-active {
  animation: slide-out .5s ease-out forwards;
  transition: opacity .5s;
  opacity: 0;
}

@keyframes slide-in{
  from{
    transform: rotateY(90deg);
  }
  to{
    transform: rotateY(0deg);
  }
}
@keyframes slide-out{
  from{
    transform: rotateY(0deg);
  }
  to{
    transform: rotateY(90deg);
  }
}
.fade-enter {
  opacity: 0;
}
.fade-enter-active {
  animation: fade-in 1s ease-out forwards;
  transition: opacity 1s;
}
.fade-leave {

}
.fade-leave-active {
  animation: fade-out 1s ease-out forwards;
  transition: opacity 1s;
  opacity: 0;
}

@keyframes fade-in{
  from{
    transform: translateX(200px);
  }
  to{
    transform: translateX(0);
  }
}
@keyframes fade-out{
  from{
    transform: translateX(0);
  }
  to{
    transform: translateX(200px);
  }
}
</style>
