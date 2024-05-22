<script setup lang="ts">
import type { SquareType } from '@/types'

type Props = {
  value: SquareType
  index: number
  winning?: boolean
}
const props = defineProps<Props>()

type Emits = {
  click: [index: number]
}

const emit = defineEmits<Emits>()
</script>

<template>
  <button
    @click="emit('click', props.index)"
    class="border border-[#999] font-bold text-2xl -mr-[1px] -mt-[1px] flex items-center justify-center w-[34px] leading-[34px] h-[34px]"
    :class="{ 'text-red-500': props.winning }"
  >
    {{ value }}
  </button>
</template>
