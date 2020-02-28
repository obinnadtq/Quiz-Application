<template>
  <div id="app">
    <Header></Header>
    <quiz-body></quiz-body>
  </div>
</template>

<script>
import Header from './components/Header.vue'
import QuizBody from './components/QuizBody.vue'

export default {
  name: 'App',
  components: {
    Header,
    QuizBody
  }
}
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
