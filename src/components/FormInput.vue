<script setup lang="ts">
import { inject } from "vue"

const props = defineProps<Props>()
interface Props {
  id?: string
  modelValue: string | number
  required?: boolean
  invalid?: boolean
  ariaDescribedBy?: string
}

const emit = defineEmits<{
  change: [id: number]
  "update:modelValue": [value: string]
}>()

const field = inject("field", props)
</script>
<template>
  <input
    :id="field.id"
    :value="props.modelValue"
    @input="($event: Event) => emit('update:modelValue', ($event.target as HTMLInputElement).value )"
    :required="field.required"
    :class="[
      'w-full rounded-md shadow-sm focus:border-blue-500 focus:ring-blue-500',
      field.invalid ? 'border-red-500' : 'border-gray-300',
    ]"
  />
</template>
