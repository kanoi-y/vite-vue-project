<script>
export default {
  data() {
    return {
      inputText: '',
      todos: [],
    }
  },
  methods: {
    addTodo() {
      if (this.inputText.trim() === '') {
        alert('ToDoが空白だと登録することが出来ません')
        return
      }
      this.todos.push({ text: this.inputText, isChecked: false })
      this.inputText = ''
    },
    deleteTodo() {
      this.todos = this.todos.filter((todo) => {
        return !todo.isChecked
      })
    },
  },
}
</script>

<template>
  <h1>My ToDo App</h1>
  <input type="text" v-model="inputText" /><button @click="addTodo">追加</button
  ><button @click="deleteTodo">完了済みを削除する</button>
  <ul v-if="todos.length !== 0">
    <li v-for="todo in todos">
      <input type="checkbox" v-model="todo.isChecked" /><span
        :class="{ 'todo-done': todo.isChecked }"
        >{{ todo.text }}</span
      >
    </li>
  </ul>
  <p v-else>ToDoがまだありません！</p>
</template>

<style>
body {
  background-color: #eee;
}

.todo-done {
  text-decoration: line-through;
}
</style>
