<template>
  <div class="quiz-body">
    <b-jumbotron>
      <template v-slot:lead>{{ currentQuestion.question }}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click.prevent="selectAnswer(index)"
          :class="answerClass(index)"
        >{{answer}}</b-list-group-item>
      </b-list-group>
      <b-button variant="primary" @click="submitAnswer" :disabled="selectedIndex === null || answered">Submit</b-button>
      <b-button variant="success" @click="next">Next</b-button>
    </b-jumbotron>
  </div>
</template>

<script>
import _ from "lodash";
export default {
  data() {
    return {
      shuffledAnswers: [],
      selectedIndex: null,
      correctIndex: null,
      answered: false
    };
  },
  props: {
    currentQuestion: Object,
    next: Function,
    increment: Function
  },
  computed: {},
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.shuffleAnswers()
        this.selectedIndex = null
        this.answered = false
      }
    }
  },
  methods: {
    shuffleAnswers() {
      let answers = [
        ...this.currentQuestion.incorrect_answers,
        this.currentQuestion.correct_answer
      ];
      this.shuffledAnswers = _.shuffle(answers);
      this.correctIndex = this.shuffledAnswers.indexOf(this.currentQuestion.correct_answer)
    },
    selectAnswer(index) {
      this.selectedIndex = index;
    },
    submitAnswer() {
      let isCorrect = false
      if (this.selectedIndex === this.correctIndex) {
        isCorrect = true
      }
      this.answered = true
      this.increment(isCorrect)
    },

    answerClass(index) {
      let answerClass = ''

      if(!this.answered && this.selectedIndex === index) {
        answerClass = 'selected'
      }
      else if(this.answered && this.correctIndex === index) {
        answerClass = 'correct'
      }
      else if(this.answered && this.selectedIndex === index && this.correctIndex !== index) {
        answerClass = 'incorrect'
      }

      return answerClass
    }
  }
};
</script>

<style scoped>
.quiz-body {
  height: 500px;
  width: 50%;
  margin: auto;
}
.list-group {
  margin-bottom: 15px;
}
button {
  margin: 5px;
}

.list-group-item:hover {
  background: #eee;
  cursor: pointer;
}

.selected {
  background-color: lightblue;
}
.correct {
  background-color: lightgreen;
}
.incorrect {
  background-color: red;
}
</style>