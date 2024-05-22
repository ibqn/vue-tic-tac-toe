<script setup lang="ts">
import Square from '@/components/square.vue'
import type { SquareType } from '@/types'
import { onMounted } from 'vue'

type Props = {
  squares: SquareType[]
  winningLine?: number[]
}
const props = defineProps<Props>()

type Emits = {
  square: [index: number]
}

const emit = defineEmits<Emits>()

onMounted(() => {
  console.log('mounted', props.squares)
})
</script>

<template>
  <div class="grid grid-cols-3 grid-rows-3 mt-[1px] mr-[1px]">
    <Square
      :value="square"
      v-for="(square, index) in squares"
      :key="index"
      :index
      @click="emit('square', index)"
      :winning="winningLine?.includes(index)"
    />
  </div>
</template>
