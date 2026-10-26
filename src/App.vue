<script setup lang="ts">
import { computed, ref } from 'vue'

let id = 0

type Todo = {
  id: number
  text: string
  done?: boolean
}

const newTodo = ref('')
const hideCompletedTodos = ref(false)
const todos = ref([
  { id: id++, text: 'Learn HTML', done: false },
  { id: id++, text: 'Learn JS', done: false },
  { id: id++, text: 'Learn Vue', done: false },
])

const filteredTodos = computed(() => {
  return hideCompletedTodos.value ? todos.value.filter((t) => !t.done) : todos.value
})

function addTodo() {
  todos.value.push({ id: id++, text: newTodo.value, done: false })
  newTodo.value = ''
}

function removeTodo(todo: Todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo" required placeholder="やることを書いてみよう！" />
    <button>リストに追加！</button>
  </form>
  <h2>現在のやることリスト一覧</h2>
  <ul>
    <li v-for="todo in filteredTodos" :key="todo.id">
      <input type="checkbox" v-model="todo.done" />
      <span :class="{ done: todo.done }">{{ todo.text }}</span>
      <button @click="removeTodo(todo)">削除</button>
    </li>
  </ul>
  <button @click="hideCompletedTodos = !hideCompletedTodos">
    {{ hideCompletedTodos ? 'すべて表示' : '完了済みタスクを隠す' }}
  </button>
</template>

<style>
.done {
  text-decoration: line-through;
}
</style>
