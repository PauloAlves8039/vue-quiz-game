<template>
  <div class="container">
    <h1 v-html="this.question" ></h1>

    <input type="radio" name="options" value="True" />
    <label>True</label>
    <br />

    <input type="radio" name="options" value="True" />
    <label>False</label>
    <br />

    <button class="send" type="button">Send</button>
  </div>
</template>

<script>
export default {
  name: "App",

  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
    }
  },

  computed: {
    answers() {
      let answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      answers.push(this.correctAnswer);
      return answers;
    }
  },

  created() {
    let url = 'https://opentdb.com/api.php?amount=1&category=18';
    this.axios.get(url)
    .then((response) => {
      this.question = response.data.results[0].question;
      this.incorrectAnswers = response.data.results[0].incorrect_answers;
      this.correctAnswer = response.data.results[0].correct_answer; 
    });
  },
};
</script>

<style lang="scss">
.container {
  text-align: center;
  max-width: 960px;
  margin: 60px auto;

  input[type="radio"] {
    margin: 12px 4px;
  }

  button.send {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    background-color: #1867c0;
    border: 1px solid #1867c0;
    cursor: pointer;
  }
}
</style>
