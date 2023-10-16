<script setup lang="ts">
import { computed, inject } from 'vue'

const props = defineProps<Props>()
interface Props {
  id?: string
  modelValue: string | number
  required?: boolean
  invalid?: boolean
  ariaDescribedBy?: string
  multiline?: boolean
}

const emit = defineEmits<{
  change: [id: number]
  'update:modelValue': [value: string]
}>()

const renderAs = computed(() => {
  return props.multiline ? 'textarea' : 'input'
})

const field = inject('field', props)
</script>
<template>
  <component
    :is="renderAs"
    :id="field.id"
    :value="props.modelValue"
    @input="
      ($event: Event) =>
        emit('update:modelValue', ($event.target as HTMLInputElement | HTMLTextAreaElement).value)
    "
    :required="field.required"
    style="width: 100%"
  />
</template>
