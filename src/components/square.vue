<script setup lang="ts">
import type { SquareType } from '@/types'
import { inject } from 'vue'

type Props = {
  value: SquareType
  index: number
  winning?: boolean
}
const props = defineProps<Props>()

const handleSquare = inject('handleSquare') as (index: number) => void
</script>

<template>
  <button
    @click="handleSquare(props.index)"
    class="border border-[#999] font-bold text-2xl -mr-px -mt-px flex items-center justify-center w-[34px] leading-[34px] h-[34px]"
    :class="{ 'text-red-500': props.winning }"
  >
    {{ value }}
  </button>
</template>
