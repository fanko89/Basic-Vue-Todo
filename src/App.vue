<template>
  <div>
    <h1>Todo App</h1>
    <div>
      <input type="text" v-model="newTodoText">
      <button @click="addTodo">Add Todo</button>
    </div>
    <ul>
      <li v-for="(todo, index) in todos" :key="todo.id">
        <input type="checkbox" v-model="todo.completed">
        <span :class="{ 'completed': todo.completed }">{{ todo.text }}</span>
        <button @click="editMode = index">Edit</button>
        <button @click="deleteTodo(index)">Delete</button>
      </li>
    </ul>
    <div v-if="editMode !== null">
      <input type="text" v-model="todos[editMode].text">
      <button @click="editMode = null">Cancel</button>
      <button @click="saveEdit">Save</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      todos: [
        { id: 1, text: 'first Item', completed: false },
        { id: 2, text: 'Second Item', completed: false } 
      ],
      newTodoText: '',
      editMode: null
    }
  },
  methods: {
    addTodo() {
      if (this.newTodoText !== '') {
        this.todos.push({
          id: this.todos.length + 1,
          text: this.newTodoText,
          completed: false
        })
        this.newTodoText = ''
      }
    },
    deleteTodo(index) {
      this.todos.splice(index, 1)
    },
    saveEdit() {
      this.editMode = null
    }
  }
}
</script>

<style>
.completed {
  text-decoration: line-through;
}
</style>