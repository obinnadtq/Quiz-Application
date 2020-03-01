<template>
  <div class="quiz-body">
    <b-jumbotron>
      <template v-slot:lead>{{ currentQuestion.question }}</template>

      <hr class="my-4" />

      <b-list-group>
        <b-list-group-item
          v-for="(answer, index) in shuffledAnswers"
          :key="index"
          @click="selectAnswer(index)"
        >{{answer}}</b-list-group-item>
      </b-list-group>
      <b-button variant="primary">Previous</b-button>
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
      selectedIndex: null
    };
  },
  props: {
    currentQuestion: Object,
    next: Function
  },
  computed: {},
  watch: {
    currentQuestion: {
      immediate: true,
      handler() {
        this.shuffleAnswers();
        this.selectedIndex = null;
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
    },
    selectAnswer(index) {
      this.selectedIndex = index;
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
</style>