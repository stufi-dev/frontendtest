<script setup lang="ts">
import { ref } from "vue";

const activeSquare = ref<number | undefined>(undefined);
const numberOfSquares = 64;
const columns = ["a", "b", "c", "d", "e", "f", "g", "h"];

const emit = defineEmits<{
  (e: "fieldPressed", field: string): void;
}>();

const getSquarePosition = (squareIndex: number) => {
  return numberOfSquares - squareIndex;
};

const getSquareRow = (squareIndex: number) => {
  const squarePosition = getSquarePosition(squareIndex);

  return Math.ceil((squarePosition + 1) / 8);
};

const getSquareColumn = (squareIndex: number) => {
  const squarePosition = getSquarePosition(squareIndex);

  return squarePosition % 8;
};

const handleSquereClick = (index: number) => {
  const row = getSquareRow(index);
  const column = getSquareColumn(index);
  emit("fieldPressed", `${columns[column]}${row}`);
  activeSquare.value = index;
};
</script>

<template>
  <div class="chess-board">
    <div
      v-for="square in numberOfSquares"
      :key="square"
      class="square"
      :class="{
        active: square === activeSquare,
      }"
      @click="handleSquereClick(square)"
    >
      <span v-if="square % 8 === 0" class="row-label">{{
        getSquareRow(square)
      }}</span>
      <span v-if="square > numberOfSquares - 8" class="column-label">{{
        columns[getSquareColumn(square)]
      }}</span>
    </div>
  </div>
</template>

<style scoped lang="scss">
.chess-board {
  display: grid;
  grid-template-columns: repeat(8, 1fr);
  direction: rtl;
  width: 500px;
  margin: 0 auto;
}

@media (max-width: 1024px) {
  .chess-board {
    width: 100%;
    max-width: 500px;
  }
}

.square {
  background-color: $dark-square;
  position: relative;
  cursor: pointer;

  &:before {
    content: "";
    display: block;
    padding-top: 100%;
  }

  &:nth-child(-2n + 8),
  &:nth-child(8) ~ &:nth-child(-2n + 15),
  &:nth-child(16) ~ &:nth-child(-2n + 24),
  &:nth-child(24) ~ &:nth-child(-2n + 31),
  &:nth-child(32) ~ &:nth-child(-2n + 40),
  &:nth-child(40) ~ &:nth-child(-2n + 47),
  &:nth-child(48) ~ &:nth-child(-2n + 56),
  &:nth-child(56) ~ &:nth-child(-2n + 63) {
    background-color: $light-square;
  }

  &.active:after {
    content: "";
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: $white;
    opacity: 0.2;
  }
}

.column-label,
.row-label {
  position: absolute;
  padding: 0.5rem;
  color: $white;
}

.row-label {
  top: 0;
  left: 0;
}

.column-label {
  bottom: 0;
  right: 0;
}
</style>
