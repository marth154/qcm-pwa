<template>
  <h2 v-if="getQuestion">{{ getQuestion.question }}</h2>
  <ul v-if="getQuestion">
    <p v-for="(answer, index) in getQuestion.answers" :key="answer">
      <button :disabled="isSubmit" v-on:click="handleAnswer(index)">
        {{ answer }}
      </button>
    </p>
  </ul>
  <p v-if="result === 'GOOD'">Good Answer</p>
  <p v-if="result === 'ERROR'">Bad Answer</p>
  <button v-if="isSubmit" v-on:click="nextQuestion()">Next</button>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import quiz from "../../mock/quiz";

export default defineComponent({
  name: "Quizz",
  data() {
    return {
      result: "",
      getQuestion:
        quiz.questions[
          Math.ceil(Math.random() * (quiz.questions.length - 0) + 0)
        ],
      isSubmit: false,
    };
  },
  methods: {
    async handleAnswer(value: number) {
      if (this.getQuestion.correctIndex === value) {
        this.result = "GOOD";
      } else {
        this.result = "ERROR";
      }
      this.isSubmit = true;
    },
    nextQuestion() {
      this.result = "";
      this.isSubmit = false;
      this.getQuestion =
        quiz.questions[
          Math.ceil(Math.random() * (quiz.questions.length - 0) + 0)
        ];
      if (this.getQuestion === undefined) {
        this.nextQuestion();
      }
    },
  },
});
</script>
