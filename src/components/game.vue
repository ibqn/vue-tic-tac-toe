<script setup lang="ts">
import { computed, provide, ref } from 'vue'
import Board from '@/components/board.vue'
import type { SquareType } from '@/types'
import { calculateWinner, isDraw } from '@/utils'

const squares = ref<SquareType[]>(Array(9).fill(null))
const move = ref(0)
const history = ref<number[]>([])

const winner = computed(() => calculateWinner(squares.value))
const isXNext = computed(() => move.value % 2 === 0)
const status = computed(() => {
  if (winner.value?.winner) {
    return `Winner: ${winner.value.winner}`
  } else if (isDraw(squares.value)) {
    return 'Draw!'
  } else {
    return `Next player: ${isXNext.value ? 'X' : 'O'}`
  }
})

const initialPosition = () => {
  squares.value = Array(9).fill(null)
  move.value = 0
  history.value = []
}

const handleSquare = (index: number) => {
  console.log('click', index)

  if (winner.value?.winner || squares.value[index]) {
    return
  }
  history.value = [...history.value.slice(0, move.value), index]
  squares.value[index] = move.value % 2 === 0 ? 'X' : 'O'
  move.value = history.value.length
}

provide('handleSquare', handleSquare)

const jumpTo = (index: number) => {
  move.value = index + 1
  squares.value = history.value.slice(0, index + 1).reduce((position, currentMove, moveIndex) => {
    position[currentMove] = moveIndex % 2 === 0 ? 'X' : 'O'
    return position
  }, Array(9).fill(null))
}
</script>

<template>
  <div class="flex flex-row p-2 gap-4">
    <div class="flex flex-col gap-2">
      <div class="flex justify-center">
        {{ status }}
      </div>

      <div class="flex p-2">
        <Board :squares :winningLine="winner?.line" />
      </div>
    </div>

    <div class="border border-slate-600"></div>

    <div class="flex flex-col gap-2">
      <button @click="initialPosition">Initial position</button>
      <template v-if="history.length">
        <h2>Moves:</h2>
        <ul>
          <li v-for="(move, index) in history" :key="index">
            <button @click="() => jumpTo(index)">
              {{ index + 1 }}. {{ index % 2 === 0 ? 'X' : 'O' }}-{{ move + 1 }}
            </button>
          </li>
        </ul>
      </template>
      <div v-else>Let's go!</div>
    </div>
  </div>
</template>
