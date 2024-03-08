<template>
  <div id="app">
    <InputForm/>
  </div>
</template>

<script>
import InputForm from './components/InputForm.vue'

export default {
  name: 'App',
  components: {
    InputForm
  }
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Montserrat:wght@500&display=swap');

body{
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}
#app{
  display: flex;
  align-items: center;
  justify-content: center;
  height: 100vh;
  width: 100vw;
  background-color: #d5d3d3;
}
</style>
