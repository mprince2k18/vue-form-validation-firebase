<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">

    <formValidate> </formValidate>

    <viewData> </viewData>

  </div>
</template>

<script>
import formValidate from './components/formValidate.vue'
import viewData from './components/viewData.vue'

export default {
  name: 'app',
  components: {
    formValidate,
    viewData
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
