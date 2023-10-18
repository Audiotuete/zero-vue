<script setup lang="ts">
import { computed, provide } from 'vue'

// @ts-expect-error
import { v4 as uuid } from 'uuid'

const props = withDefaults(defineProps<Props>(), {
  id: () => `field-${uuid()}`
})
interface Props {
  id?: string
  label?: string
  required?: boolean
  error?: string
  help?: string
}

const ariaDescribedBy = computed(() => {
  return !!props.help ? `help-${uuid()}` : undefined
})

provide(
  'field',
  computed(() => {
    return {
      ...props,
      invalid: !!props.error,
      ariaDescribedBy: ariaDescribedBy.value
    }
  })
)
</script>

<template>
  <div>
    <label v-if="props.label" :for="props.id" :required="props.required">
      {{ props.label }}<span v-if="props.required">*</span>
    </label>

    <slot v-bind="props" />

    <p v-if="props.error">
      {{ props.error }}
    </p>

    <p v-if="props.help" :id="ariaDescribedBy">
      {{ props.help }}
    </p>
  </div>
</template>
