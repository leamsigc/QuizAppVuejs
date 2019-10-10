<template>
  <div id="app">
    <Header />
    <QuizBox />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import QuizBox from "./components/QuizBox.vue";

export default {
  name: "app",
  components: {
    Header,
    QuizBox
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
  height: 10vh;
}
</style>
