<script setup lang="ts">
import { ref } from 'vue'
import ChildComp from './components/ChibiComp.vue'

const greeting = ref('Hello from 親コンポーネント')
</script>

<template>
  <ChildComp :msg="greeting" />
</template>
