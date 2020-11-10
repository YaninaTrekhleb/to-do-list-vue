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
      v-for="(todo, index) in todos" 
      :key="todo.id" 
      class="todo-item"
    >
      <div class="todo-item-left">
        <input 
          type="checkbox"
          v-model="todo.completed"
        >
        <div 
          v-if="!todo.editing"
          @dblclick="editToDo(todo)"
          class="todo-item-lable"
          :class="{ completed : todo.completed }"
        >
          {{ todo.title }}
        </div>
        <input 
          type="text" 
          v-else
          v-model="todo.title"
          class="todo-item-edit"
          @blur="doneEdit(todo)"
          @keyup.enter="doneEdit(todo)"
          v-focus
          @keyup.esc="cancelEdit(todo)"
        >
      </div>
      <div 
        class="remove-item"
        @click="removeToDo(index)"
      >
        &times;
      </div>
    </div>

    <div class="extra-container">
      <div>
        <label>
          <input 
            type="checkbox"
          > 
          Check All
        </label>
      </div>
      <div>
        {{ remaining }} items left
      </div>
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
      beforeEditCache: '',
      todos: [
        {
          id: 1,
          title: 'Make course ready',
          completed: false,
          editing: false
        },
        {
          id: 2,
          title: 'Water Flowers',
          completed: false,
          editing: false
        },
      ]
    }
  },
  computed: {
    remaining() {
      return this,this.todos.filter(todo => !todo.completed).length
    } 
  },
  directives: {
    focus: {
      inserted: function (el) {
        el.focus()
      }
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
    },
    removeToDo(index) {
      this.todos.splice(index, 1)
    },
    editToDo(todo) {
      this.beforeEditCache = todo.title
      todo.editing = true
    },
    doneEdit(todo) {
      if (todo.title.trim() == '') {
        todo.title = this.beforeEditCache
      }
      todo.editing = false
    },
    cancelEdit(todo) {
      todo.title = this.beforeEditCache
      todo.editing = false
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

  .todo-item {
    display: flex;
    flex-direction: row;
    justify-content: space-between;
  }

  .remove-item {
    cursor: pointer;
    margin-left: 14px;  /* ? */
  }

  &:hover {
    color: black;
  }

  .todo-item-edit {
    font-size: 24px;
    color: #2c3e50;
    margin-left: 12px;
    width: 100%;
    padding: 10px;
    border: 1px solid #ccc;
    font-family: 'Avenir', Arial, Helvetica, sans-serif;
  }

  .completed {
    text-decoration: line-through;
    color: grey;
  }

  .extra-container {
    display: flex;
    align-items: center;
    justify-content: space-between;
    font-size: 16px;
    border-top: 1px solid lightgrey;
    padding-top: 14px;
    margin-bottom: 14px;
  }
</style>
