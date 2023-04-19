<script setup lang="ts">
import { ref } from 'vue'
import RoundRobin from '../src/components/RoundRobin.vue'
import GameMessage from './components/GameMessage.vue'

// アクティブプレイヤー
const playerId = ref(1)

// ボードの初期状態
const initStates: Array<Array<number>> = [
  [-1, -1, -1],
  [-1, -1, -1],
  [-1, -1, -1],
]
const states = ref(initStates)

/**
 * ボード選択
 *
 * @param rowsIndex 行番号
 * @param colsIndex 列番号
 */
const onSelect = (rowsIndex: number, colsIndex: number) => {
  let board = states.value
  if (board[rowsIndex][colsIndex] == -1) {
    board[rowsIndex][colsIndex] = Number(playerId.value)
    playerId.value = Number(playerId.value) === 1 ? 2 : 1
  } else {
    alert('そのマスは、すでに選択されています！')
  }
  states.value = board
}
</script>

<template>
  <RoundRobin :states="states" @onSelect="onSelect" />
  <GameMessage :playerId="playerId" />
</template>
