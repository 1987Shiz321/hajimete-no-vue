<script setup lang="ts">
import { ref } from 'vue'
import ChildComp from './components/ChibiComp.vue'

const childMsg = ref('No child msg yet')
</script>

<template>
  <ChildComp @response2="(msg) => (childMsg = msg)" />
  <p>{{ childMsg }}</p>
</template>
