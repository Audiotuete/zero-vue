<script setup lang="ts">
import { computed } from 'vue'

const props = defineProps({
  ratio: {
    type: String,
    default: '1:1',
    validator: (v: string) => {
      const [w, h] = v.split(':').map((v) => parseInt(v))
      return !Number.isNaN(w) && !Number.isNaN(h)
    }
  },
  maxWidth: String
})

const compPaddingTop = computed(() => {
  const [w, h] = props.ratio.split(':').map((v) => parseInt(v))
  return { paddingTop: (h / w) * 100 + '%' }
})
</script>

<template>
  <div :style="{ maxWidth: props.maxWidth }">
    <div class="aspect-ratio-container-inner" :style="compPaddingTop">
      <slot />
    </div>
  </div>
</template>

<style>
.aspect-ratio-container-inner {
  position: relative;
  overflow: hidden;
  width: 100%;
}

.aspect-ratio-container-inner > * {
  object-fit: cover;
  position: absolute;
  top: 0;
  left: 0;
  bottom: 0;
  right: 0;
  width: 100%;
  height: 100%;
}
</style>
