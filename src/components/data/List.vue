<script setup lang="ts">
import { computed, type StyleValue } from 'vue'

const props = defineProps<Props>()
interface Props {
  row?: boolean
  wrapReverse?: boolean
  wrap?: boolean
}
const direction = computed(() => {
  props.row ? 'row' : 'column'
})

const wrapIt = computed(() => {
  if (props.wrapReverse) {
    return 'wrap-reverse'
  }
  return props.wrap && 'wrap'
})
</script>

<template>
  <ul
    class="list"
    :style="
      {
        flexWrap: wrapIt,
        flexDirection: direction
      } as StyleValue
    "
  >
    <slot></slot>
  </ul>
</template>

<style scoped>
.list {
  overflow: auto;
  display: flex;
  width: 100%;
}
</style>
