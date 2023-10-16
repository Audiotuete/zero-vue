<script setup lang="ts">
const props = defineProps({
  for: String,
  required: Boolean,
})
</script>
<template>
  <label
    class="mb-1 inline-block text-sm font-medium text-gray-700"
    :for="props.for"
  >
    <slot /><span
      class="text-red-600"
      v-if="props.required"
      >*</span
    >
  </label>
</template>
