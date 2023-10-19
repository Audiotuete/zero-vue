<script setup lang="ts">
import { computed } from 'vue'

const props = withDefaults(defineProps<Props>(), {
  lineHeight: '1.5'
})
interface Props {
  size?: string
  color?: string
  align?: 'center' | 'right' | 'left' | 'justify'
  transform?: 'none' | 'capitalize' | 'uppercase' | 'lowercase' | 'full-width' | 'full-size-kana'
  inline?: boolean
  hyphens?: boolean
  lineHeight?: string
}
const renderAs = computed(() => {
  return props.inline ? 'span' : 'p'
})

const hyphenate = computed(() => {
  return props.hyphens ? 'auto' : 'none'
})
</script>

<template>
  <component
    class="text"
    :is="renderAs"
    :style="{
      color: props.color,
      fontSize: props.size,
      lineHeight: props.lineHeight,
      hyphens: hyphenate,
      textAlign: props.align,
      textTransform: props.transform
    }"
  >
    <slot></slot>
  </component>
</template>
