<script setup lang="ts">
import { ref, computed } from 'vue'

type Todo = {
  id: number
  text: string
  isCompleted: boolean
}

let id = 0
//ここにはタスク名だけが入る
const newTodo = ref('')
//完了済みのタスクを表示するかのトグル
const isDisplayCompleted = ref(true)

//タスク一覧
const todos = ref<Todo[]>([
  { id: id++, text: 'Vueの配列操作を学ぶ', isCompleted: false },
  { id: id++, text: 'Lesson 1を復習する', isCompleted: false },
  { id: id++, text: 'TypeScriptの型を定義する', isCompleted: false },
])

//タスク一覧(フィルター用)
const filteredTodos = computed(() => {
  return isDisplayCompleted.value ? todos.value : todos.value.filter((t) => !t.isCompleted)
})

const completedTasks = computed(() => {
  return todos.value.filter((t) => t.isCompleted).length
})

function addTodo() {
  //空白のみのTodo名を弾く
  if (newTodo.value.trim() !== '') {
    todos.value.push({ id: id++, text: newTodo.value.trim(), isCompleted: false })
    newTodo.value = ''
  }
}

function removeTodo(todo: Todo) {
  todos.value = todos.value.filter((t) => t.id !== todo.id)
}
</script>

<template>
  <main>
    <h1>My Todo List</h1>

    <form @submit.prevent="addTodo">
      <input v-model="newTodo" required placeholder="新しいTodoを入力..." />
      <button>追加</button>
    </form>

    <button @click="isDisplayCompleted = !isDisplayCompleted">
      {{ isDisplayCompleted ? '完了済みタスクを隠す' : '完了済みタスクを表示する' }}
    </button>

    <!-- ここにUIを実装する -->
    <ul>
      <li v-for="todo in filteredTodos" :key="todo.id">
        <input type="checkbox" v-model="todo.isCompleted" />
        <span :class="{ isCompleted: todo.isCompleted }">{{ todo.text }}</span>
        <button @click="removeTodo(todo)">削除</button>
      </li>
    </ul>

    <p>全タスク:{{ todos.length }}件</p>
    <p>完了済み:{{ completedTasks }}件</p>
    <p>未完了:{{ todos.length - completedTasks }}件</p>
  </main>
</template>

<style>
/* 必要であれば自由にスタイリングしてOK */
.isCompleted {
  text-decoration: line-through;
}
</style>
