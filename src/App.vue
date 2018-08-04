<template>
  <div id="app" class="flex-column justify-center align-center">
    <calculator></calculator>
  </div>
</template>

<script>
import Calculator from './components/Calculator';

export default {
  name: 'app',
  components: {
    Calculator
  }
};
</script>

<style>
*,
*:before,
*:after {
  box-sizing: border-box;
}

body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #262525;
  width: 100vw;
  height: 100vh;
  background-color: #fff6da;
}

.flex-row {
  display: flex;
  flex-direction: row;
}

.flex-column {
  display: flex;
  flex-direction: column;
}

.justify-start {
  justify-content: flex-start;
}

.justify-center {
  justify-content: center;
}

.justify-end {
  justify-content: flex-end;
}

.align-center {
  align-items: center;
}
</style>
