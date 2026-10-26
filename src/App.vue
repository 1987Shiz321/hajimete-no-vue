<script setup lang="ts">
import { ref, watch } from 'vue'

const todoId = ref(1)
const todoData = ref(null)

async function fetchData() {
  // 出力されるDOM要素の部分を一度nullにする⇒v-ifの要素が表示
  todoData.value = null

  const res = await fetch(`https://jsonplaceholder.typicode.com/todos/${todoId.value}`)
  // レスポンスをtodoData.valueに代入してDOM要素の更新⇒v-elseの要素が表示
  todoData.value = await res.json()
}

// 初回のデータを取得する
fetchData()

//watch(監視するデータ, 変更されたときに実行する関数)
//todoIdが変わったらfetchDataを実行してねーという意味
watch(todoId, fetchData)
</script>

<template>
  <p>Todo id: {{ todoId }}</p>
  <button @click="todoId++" :disabled="!todoData">Fetch next todo</button>
  <!-- null担っている間はv-ifが表示される -->
  <p v-if="!todoData">Loading...</p>
  <pre v-else>{{ todoData }}</pre>
</template>
