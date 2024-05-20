<script setup lang="ts">
import Square from '@/components/square.vue'
import { ref, onMounted } from 'vue'

type SquareType = string | null

const squares = ref<SquareType[]>(Array(9).fill(null))
const isXNext = ref(true)

const handleSquareClick = (index: number) => {
  console.log('click', index)
  if (isXNext.value) {
    squares.value[index] = 'X'
  } else {
    squares.value[index] = 'O'
  }
  isXNext.value = !isXNext.value
}

onMounted(() => {
  console.log('mounted', squares.value)
})
</script>

<template>
  <div class="grid grid-cols-3 grid-rows-3 mt-[1px] mr-[1px]">
    <Square
      :value="square"
      v-for="(square, index) in squares"
      :key="index"
      :index
      @click="handleSquareClick"
    />
  </div>
</template>
