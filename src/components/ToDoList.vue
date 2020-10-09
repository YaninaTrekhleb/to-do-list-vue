<template>
  <div id="todo-list">
    <h2>To Do List Tasks</h2>
    <input 
      type="text" 
      class="todo-input" 
      placeholder="What needs to be done"
      v-model="newTodo"
      @keyup.enter="addNewToDo"
    >
    <div 
      v-for="todo in todos" 
      :key="todo.id" 
      class="todo-item"
    >
      {{ todo.title }}
    </div>
  </div>
</template>

<script>


export default {
  name: 'ToDoList',
  data () {
    return {
      newTodo: '',
      idForTodo: 3,
      todos: [
        {
          id: 1,
          title: 'Make course ready',
          completed: false
        },
        {
          id: 2,
          title: 'Water Flowers',
          completed: false
        },
      ]
    }
  },
  methods: {
    addNewToDo() {
      if (this.newTodo.trim().length == 0) {
        return
      }

      this.todos.push({
        id: this.idForTodo,
        title: this.newTodo,
        completed: false
      })

      this.newTodo = ''
      this.idForTodo++
    }
  }
}
</script>

<style>
  .todo-input {
    width: 100%;
    padding: 10px 18px;
    font-size: 1.2em;
  }
</style>
