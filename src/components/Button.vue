<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps<Props>()
interface Props {
  iconLeft?: object
  iconRight?: object
  loading?: boolean
  disabled?: boolean
  href?: string
}
const renderAs = computed(() => {
  return props.href ? 'a' : 'button'
})
</script>

<template>
  <component :is="renderAs" :href="props.href" :disabled="props.disabled">
    <component v-if="!props.loading" :is="props.iconLeft" />
    <span v-if="!props.loading">
      <slot />
    </span>

    <component :is="props.iconRight" v-if="!props.loading" />
    <span v-if="props.loading">Loading...</span>
  </component>
</template>
