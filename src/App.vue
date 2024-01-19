<script setup lang="ts">
import { ref } from "vue";
import ChessBoard from "./components/ChessBoard.vue";
import MovesHistory from "./components/MovesHistory.vue";

const history = ref<Array<string>>([]);

const handleFieldPressed = (field: string) => {
  history.value = [...history.value, field];
};
</script>

<template>
  <div class="app">
    <main>
      <ChessBoard @field-pressed="handleFieldPressed" />
    </main>
    <aside class="sidebar">
      <MovesHistory :history="history" />
    </aside>
  </div>
</template>

<style scoped lang="scss">
.app {
  display: flex;
  margin: 2rem;
  gap: 2rem;
}

.sidebar {
  flex: 1;
  background-color: $dark-gray;
}

.chessboard-wrapper {
  max-height: 100vh;
}

@media (max-width: 1024px) {
  .app {
    flex-direction: column;
  }
}
</style>
