<template>
  <div id="app">
    <h1>Main Title in APP</h1>
    <ToDoList />
  </div>
</template>

<script>
import ToDoList from './components/ToDoList'

export default {
  name: 'App',
  components: {
    ToDoList
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  display: flex;
  justify-content: center;
  flex-direction: column;
  text-align: center;
  margin: 0 auto;
  width: 60%;
  font-size: 24px;
}
</style>
