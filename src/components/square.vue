<script setup lang="ts">
type Props = {
  value: string | null
  index: number
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
  >
    {{ value }}
  </button>
</template>
