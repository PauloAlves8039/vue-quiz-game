<template>
  <div class="container">
    <ScoreBoard :winCount="this.winCount" :loseCount="this.loseCount" />

    <template v-if="this.question">
      <h1 v-html="this.question"></h1>

      <template v-for="(answer, index) in this.answers" :key="index">
        <input
          :disabled="this.answerSubmitted"
          type="radio"
          name="options"
          :value="answer"
          v-model="this.chosenAnswer"
        />
        <label v-html="answer"></label><br />
      </template>

      <button @click="this.submitAnswer()" class="send" type="button">
        Send
      </button>

      <section class="result" v-if="this.answerSubmitted">
        <template v-if="this.chosenAnswer == this.correctAnswer">
          <h4 v-html="'&#9989; Congratulations, the answer ' + this.correctAnswer + ' is correct.'"></h4>
        </template>
        <template v-else>
          <h4 v-html="'&#10060; I´m Sorry, you picked the wrong answer. The correct is' + this.correctAnswer + '.' "></h4>
        </template>
        <button @click="this.getNewQuestion()" class="send" type="button">
          Next question
        </button>
      </section>
    </template>
  </div>
</template>

<script>
import ScoreBoard from "@/components/ScoreBoard.vue";

export default {
  name: "App",
  components: {
    ScoreBoard,
  },

  data() {
    return {
      question: undefined,
      incorrectAnswers: undefined,
      correctAnswer: undefined,
      chosenAnswer: undefined,
      answerSubmitted: false,
      winCount: 0,
      loseCount: 0,
    };
  },

  computed: {
    answers() {
      let answers = JSON.parse(JSON.stringify(this.incorrectAnswers));
      answers.splice(Math.round(Math.random() * answers.length), 0, this.correctAnswer);
      return answers;
    },
  },

  methods: {
    submitAnswer() {
      if (!this.chosenAnswer) {
        alert("Pick one of the options.");
      } else {
        this.answerSubmitted = true;
        if (this.chosenAnswer == this.correctAnswer) {
          this.winCount++;
        } else {
          this.loseCount++;
        }
      }
    },

    getNewQuestion() {
      this.answerSubmitted = false;
      this.chosenAnswer = undefined;
      this.question = undefined;

      let url = "https://opentdb.com/api.php?amount=1&category=18";

      this.axios.get(url).then((response) => {
        this.question = response.data.results[0].question;
        this.incorrectAnswers = response.data.results[0].incorrect_answers;
        this.correctAnswer = response.data.results[0].correct_answer;
      });
    },
  },

  created() {
    this.getNewQuestion();
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
    color: #1867c0;
    font-weight: 600;
    background-color: #fff;
    border: 1px solid #101010;
    cursor: pointer;
  }
  button.send:hover {
    margin-top: 12px;
    height: 40px;
    min-width: 120px;
    padding: 0 16px;
    color: #fff;
    font-weight: 600;
    background-color: #1867c0;
    border: 1px solid #101010;
    transition: 1s;
    cursor: pointer;
  }
}

.result {
  font-weight: 600;
}
</style>
