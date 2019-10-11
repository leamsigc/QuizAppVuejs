<template>
  <header class="header">
    <div class="container">
      <div class="logo">
        Vuejs
        <span>QuizApp</span>
      </div>
      <div class="count">
        <small>Count:</small>
        0/10
      </div>
    </div>
  </header>
</template>

<script>
export default {
  name: "Header"
};
</script>

<style >
.header {
  background: var(--white-color);
  padding: 1rem 2rem;
}
.header .container {
  width: 100%;
  display: flex;
  justify-content: space-between;
  align-items: center;
  flex-wrap: wrap;
}
.logo {
  color: var(--secondary-color);
  font-weight: 900;
}
.logo span {
  color: var(--logo-color);
}
</style>