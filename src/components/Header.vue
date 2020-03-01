<template>
  <div class="header">
    <h1>Quiz Application</h1>
    <h6>Counter: {{ numCorrect }}/{{ numTotal }}</h6>
  </div>
</template>

<script>
export default {
  props: ["numCorrect", "numTotal"]
};
</script>

<style scoped>
</style>
