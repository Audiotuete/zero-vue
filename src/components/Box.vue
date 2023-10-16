<script setup lang="ts">
import { computed, type StyleValue } from 'vue'

const props = defineProps<Props>()
interface Props {
  row?: boolean
  reverse?: boolean
  wrap?: boolean
  justify?: 'center' | 'flex-start' | 'flex-end' | 'space-between' | 'space-around' | 'space-evenly'
  align?: 'center' | 'flex-start' | 'flex-end'
  flex?: string
}
const direction = computed(() => {
  const dir = props.row ? 'row' : 'column'

  return dir
})

const wrapIt = computed(() => {
  return props.wrap && 'wrap'
})
</script>

<template>
  <div
    :class="{ box: true }"
    :style="
      {
        flexDirection: direction,
        justifyContent: props.justify,
        alignItems: props.align,
        flexWrap: wrapIt,
        flex: props.flex
      } as StyleValue
    "
  >
    <slot></slot>
  </div>
</template>

<style scoped>
.box {
  display: flex;
  width: 100%;
  padding: 10px;
  height: 100%;
  border: 1px solid black;
}
</style>
