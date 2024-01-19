<script setup lang="ts">
defineProps<{
  history: Array<string>;
}>();
</script>

<template>
  <ol class="history-list">
    <li v-for="(historyEvent, index) in history" :key="index">
      {{ `${index + 1}.` }}
      {{ historyEvent }}
    </li>
  </ol>
</template>

<style scoped lang="scss">
.history-list {
  padding: 1rem;

  li {
    display: inline-block;
    margin-left: 0.3rem;
  }
}
</style>
