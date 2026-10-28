<script setup lang="ts">
import { ref, computed } from 'vue'

// ここに処理を実装する
const maxValue = 10
const minValue = 0
//refで状態を管理する
const count = ref(0)

//messageはcountの状態によって定められるのでcomputedを使う
const message = computed(() => {
  if (count.value === maxValue) {
    return '最大値に到達しています'
  }

  if (count.value === minValue) {
    return '最小値に到達しています'
  }

  return `あと${maxValue - count.value}回増やせます`
})

function increment() {
  if (count.value < maxValue) {
    count.value++
  }
}

function decrement() {
  if (count.value > minValue) {
    count.value--
  }
}

function reset() {
  count.value = 0
}
</script>

<template>
  <main>
    <h1>Vue Counter</h1>

    <!-- ここにUIを実装する -->
    <div>
      <p>{{ count }}</p>
      <button @click="decrement" :disabled="count === minValue">-</button>
      <button @click="increment" :disabled="count === maxValue">+</button>
      <button @click="reset" :disabled="count === minValue">reset</button>
      <p>{{ message }}</p>
    </div>
  </main>
</template>

<style>
/* 必要であれば自由にスタイリングしてOK */
</style>
