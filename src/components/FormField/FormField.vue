<script setup lang="ts">
import FormFieldLabel from "./FormFieldLabel.vue"
import FormFieldErrorMsg from "./FormFieldErrorMsg.vue"
import FormFieldHelperMsg from "./FormFieldHelperMsg.vue"
import { computed, provide } from "vue"

// @ts-expect-error
import { v4 as uuid } from "uuid"

const props = withDefaults(defineProps<Props>(), {
  id: () => `field-${uuid()}`,
})
interface Props {
  id?: string
  label?: string
  required?: boolean
  error?: string
  help?: string
}

const ariaDescribedBy = computed(() => {
  return !!props.help ? `help-${uuid()}` : null
})

provide(
  "field",
  computed(() => {
    return {
      ...props,
      invalid: !!props.error,
      ariaDescribedBy: ariaDescribedBy.value,
    }
  })
)
</script>

<template>
  <div>
    <FormFieldLabel
      v-if="props.label"
      :for="props.id"
      :required="props.required"
      >{{ props.label }}</FormFieldLabel
    >

    <slot v-bind="props" />

    <FormFieldErrorMsg v-if="props.error">
      {{ props.error }}
    </FormFieldErrorMsg>

    <FormFieldHelperMsg
      v-if="props.help"
      :id="ariaDescribedBy"
    >
      {{ props.help }}
    </FormFieldHelperMsg>
  </div>
</template>
