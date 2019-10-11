<template>
  <div id="app">
    <Header :CurrentIndex="correctAnswers" />
    <QuizBox
      v-if="AllQuiz"
      :CurrentQuiz="AllQuiz[CurrentIndex]"
      v-on:handleNext="handleNext"
      v-on:correctAnswersChecker="correctAnswersChecker"
    />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuizBox from "./components/QuizBox.vue";

export default {
  name: "app",
  data: function() {
    return {
      correctAnswers: 0,
      CurrentIndex: 0,
      AllQuiz: null
    };
  },
  methods: {
    handleNext() {
      this.CurrentIndex >= this.AllQuiz.length
        ? (this.CurrentIndex = 0)
        : this.CurrentIndex++;
    },
    correctAnswersChecker(isCorrect) {
      if (isCorrect) {
        this.correctAnswers++;
      }
    }
  },
  components: {
    Header,
    QuizBox
  },
  mounted: function() {
    fetch("https://opentdb.com/api.php?amount=10&difficulty=easy&type=multiple")
      .then(res => res.json())
      .then(res => {
        this.AllQuiz = res.results;
      });
  }
};
</script>

<style>
:root {
  --main-font: "Poppins", sans-serif;

  --white-color: #fff;
  --backgound-color: #dee0e6;
  --main-color: #134e6f;
  --secondary-color: #ffa822;
  --logo-color: #1ac0c6;
  --danger-color: tomato;
}
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
html,
body {
  font-size: 20px;
  background: var(--backgound-color);
}
#app {
  font-family: var(--main-font);
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: var(--main-font);
  height: 10;
}
.container {
  max-width: 1200px;
  margin: 0 auto;
}
.dp-f {
  display: flex;
  justify-content: center;
  align-items: center;
}
.btn {
  background: var(--white-color);
  padding: 0.5rem 1.5rem;
  border: none;
  color: var(--secondary-color);
  font-weight: 900;
  font-size: 1rem;
  border-radius: 0.3rem;

  display: inline-block;
  cursor: pointer;
  transition: border 0.3s ease-in-out, background 0.3s ease-in-out,
    color 0.2s ease-in-out;
}

.btn-primary {
  background: var(--secondary-color);
  color: var(--white-color);
  border: 1px solid transparent;
}
.btn-primary:hover,
.btn-primary:active {
  background: var(--white-color);
  color: var(--secondary-color);
  border-color: var(--secondary-color);
}
.btn-secondary {
  border: 1px solid var(--secondary-color);
}
.btn-secondary:hover,
.btn-secondary:active {
  background: var(--secondary-color);
  color: var(--white-color);
}
</style>
