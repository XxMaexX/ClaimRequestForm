<template>
  <div id="app">
    <img src="./assets/logo.png">
    <Title/>
    <BasicForm/>
  </div>
</template>

<script>
import BasicForm from './components/BasicForm.vue';
import Title from './components/Title.vue'


export default {
  name: 'app',
  components: {
    BasicForm,
    Title
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
