<!--/////////////////////////////////////////////
//                                             //
// Edit & Design by White Bear (@howaitokuma). //
// Raihan Hafiizh Qurratu'Ain                  //
//                                             //
///////////////////////////////////////////////// -->

<template>
  <div id="app" class="container">
    <h1>TO DO LIST</h1>
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    <todo-list></todo-list>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'
import TodoList from './components/TodoList.vue'

export default {
  name: 'app',
  components: {
    HelloWorld,
    TodoList,
  }
}
</script>

<style>

* {
  box-sizing: border-box;
}

.container {
  max-width: 600px;
  margin: 0 auto;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  /* text-align: center; */
  color: #2c3e50;
  margin-top: 60px;
  font-size: 25px;
}

h1{
  text-align: center;
  font-family: 'Lucida Console';
}
</style>
