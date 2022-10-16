<script>
import TodoAdd from '@/components/components/TodoAdd.vue'
import TodoList from '@/components/components/TodoList.vue'
import { useTodosStore } from '@/stores/todos'
import { mapActions, mapStores } from 'pinia'

export default {
  components: {
    TodoAdd,
    TodoList,
  },
  computed: {
    ...mapStores(useTodosStore),
    countDoneTodos() {
      const store = useTodosStore()
      return store.countDoneTodos
    },
  },
  methods: {
    ...mapActions(useTodosStore, ['addTodo', 'clearDoneTodos']),
    addNewTodo(newTodoText) {
      if (!newTodoText) return alert('文字を入力してください')
      this.addTodo({
        isDone: false,
        text: newTodoText,
      })
    },
  },
}
</script>

<template>
  <p>{{ countDoneTodos  }}</p>
  <TodoAdd @delete-done="clearDoneTodos" @add-todo="addNewTodo" />
  <p v-if="todosStore.todos.length === 0">ToDoがまだありません！</p>
  <TodoList v-else :todos="todosStore.todos" />
</template>

<style>
.todo-done {
  text-decoration: line-through;
}
</style>
