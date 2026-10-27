<script setup lang="ts">
const emit = defineEmits(['response2'])

emit('response2', 'hello from child')
</script>

<template>
  <h2>Child Component</h2>
</template>
