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
    <component :is="props.iconLeft" :class="['mr-2 h-5 w-5', props.loading && 'invisible']" />

    <span :class="[props.loading && 'invisible']">
      <slot />
    </span>

    <component
      :is="props.iconRight"
      v-if="!props.loading"
      :class="['ml-2 h-5 w-5', props.loading && 'invisible']"
    />
    <svg
      v-if="props.loading"
      class="absolute h-5 w-5 animate-spin"
      xmlns="http://www.w3.org/2000/svg"
      fill="none"
      viewBox="0 0 24 24"
    >
      <circle
        class="opacity-25"
        cx="12"
        cy="12"
        r="10"
        stroke="currentColor"
        stroke-width="4"
      ></circle>
      <path
        class="opacity-75"
        fill="currentColor"
        d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z"
      ></path>
    </svg>
  </component>
</template>
