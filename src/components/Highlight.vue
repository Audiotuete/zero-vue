<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<Props>()
interface Props {
  bold?: boolean
  italic?: boolean
  underline?: boolean
  strike?: boolean
}
const renderAs = computed(() => {
  if (props.bold) {
    return 'strong'
  } else if (props.italic) {
    return 'em'
  } else if (props.strike) {
    return 's'
  } else {
    return 'span'
  }
})
</script>

<template>
  <component
    :is="renderAs"
    :class="{
      underline: props.underline
    }"
  >
    <slot />
  </component>
</template>

<style scoped>
.underline {
  text-decoration: underline;
}
</style>
