<template>
  <div class="container dp-f">
    <div class="quiz-container">
      <h2 class="quiz__title" v-html="CurrentQuiz.question"></h2>
      <p>Posible Answers:</p>
      <ul class="quiz__options">
        <li
          class="quiz__options--item"
          v-bind:key="item"
          v-for=" item in allAnswers"
          @click.prevent="selectedItem(item)"
          :class="[!submited && item === itemSelected ? 'active': 
          submited && correctAnswer === item  ? 'correct': submited && itemSelected !== CurrentQuiz.correct_answer && item === itemSelected ? 'incorrect':'']"
        >{{item}}</li>
      </ul>
      <div class="btn-container">
        <button
          class="btn btn-primary"
          @click="submitAnswer"
          :disabled="itemSelected === null || submited "
        >Submit</button>
        <button :disabled="!submited " class="btn btn-secondary" @click="$emit('handleNext')">Next</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: "QuizBox",
  data: function() {
    return {
      itemSelected: null,
      suffleAllAnswers: null,
      submited: false,
      correctAnswer: this.CurrentQuiz.correct_answer
    };
  },
  props: ["CurrentQuiz"],
  watch: {
    CurrentQuiz() {
      this.correctAnswer = this.CurrentQuiz.correct_answer;
      this.itemSelected = null;
      this.submited = false;
      this.suffleAnswers();
    }
  },
  computed: {
    allAnswers() {
      let answers = [
        ...this.CurrentQuiz.incorrect_answers,
        this.CurrentQuiz.correct_answer
      ];
      return this.shuffle(answers);
    }
  },
  methods: {
    selectedItem(item) {
      this.itemSelected = item;
    },
    submitAnswer() {
      let isCorrect = false;
      if (this.itemSelected === this.CurrentQuiz.correct_answer) {
        isCorrect = true;
        this.$emit("correctAnswersChecker", isCorrect);
      }
      this.submited = true;
    },
    shuffle(a) {
      for (let i = a.length - 1; i > 0; i--) {
        const j = Math.floor(Math.random() * (i + 1));
        [a[i], a[j]] = [a[j], a[i]];
      }
      return a;
    },
    suffleAnswers() {
      let answers = [
        ...this.CurrentQuiz.incorrect_answers,
        this.CurrentQuiz.correct_answer
      ];
      answers = this.shuffle(answers);
      this.suffleAllAnswers = answers;
    }
  }
};
</script>

<style>
.quiz-container {
  max-width: 700px;
  width: 100%;
  min-width: 400px;
  margin-top: 15vh;
  background: var(--white-color);
  color: var(--main-color);
  padding: 2rem;
  border-radius: 0.5rem;
  line-height: 1.5;
}
.quiz__title {
  font-weight: 400;
  padding: 1rem 0;
  font-size: 1rem;
}
p {
  text-align: left;
  font-weight: 700;
  opacity: 0.7;
  margin-bottom: 1rem;
}
.quiz__options {
  text-align: left;
  padding: 1rem 2rem;
  list-style: none;
}
.quiz__options--item {
  position: relative;
  font-weight: 300;
  padding: 0.5rem;
  transition: backgound 0.3s ease-in-out;
  cursor: pointer;
}
.active,
.quiz__options--item:hover {
  background: var(--backgound-color);
}
.correct {
  background: var(--logo-color);
}
.incorrect {
  background: var(--danger-color);
}
.quiz__options--item:before {
  content: "";
  display: block;
  width: 0.5rem;
  height: 0.5rem;
  border-radius: 50%;
  background: var(--secondary-color);

  position: absolute;
  top: 1rem;
  left: -1rem;
}
.btn-container {
  display: flex;
  justify-content: flex-end;
}
.btn-container .btn-secondary {
  margin-left: 1rem;
}
button:disabled,
button[disabled] {
  cursor: none;
  border: 1px solid #999999;
  background-color: #cccccc;
  color: #666666;
}
</style>