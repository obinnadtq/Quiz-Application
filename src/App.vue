<template>
  <div id="app">
    <Header :numCorrect="numCorrect" :numTotal="numTotal"></Header>
    <quiz-body
      v-if="questions.length"
      :currentQuestion="questions[index]"
      :next="next"
      :increment="increment"
    ></quiz-body>
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuizBody from "./components/QuizBody.vue";
import axios from "axios";

export default {
  name: "App",
  components: {
    Header,
    QuizBody
  },
  data() {
    return {
      questions: [],
      index: 0,
      numCorrect: 0,
      numTotal: 0
    };
  },
  methods: {
    next() {
      this.index++;
    },
    increment(isCorrect) {
      if (isCorrect) {
        this.numCorrect++;
      }
      this.numTotal++;
    }
  },

  mounted() {
    axios
      .get(
        "https://opentdb.com/api.php?amount=50&category=18&difficulty=medium&type=multiple"
      )
      .then(response => {
        this.questions = response.data.results;
      });
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
