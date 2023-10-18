<script setup lang="ts">
import { computed, type StyleValue } from 'vue'

const props = defineProps<Props>()
interface Props {
  h?: string
  w?: string
  m?: string
  p?: string
  row?: boolean
  reverse?: boolean
  wrap?: boolean
  justify?: 'center' | 'flex-start' | 'flex-end' | 'space-between' | 'space-around' | 'space-evenly'
  align?: 'center' | 'flex-start' | 'flex-end'
  flex?: string
  as?: 'header' | 'footer' | 'main' | 'article' | 'section' | 'aside'
}
const direction = computed(() => {
  const dir = props.row ? 'row' : 'column'

  return dir
})

const wrapIt = computed(() => {
  return props.wrap && 'wrap'
})

const renderAs = computed(() => {
  return props.as ? props.as : 'div'
})
</script>

<template>
  <component
    :is="renderAs"
    :class="{ box: true }"
    :style="
      {
        flexDirection: direction,
        justifyContent: props.justify,
        alignItems: props.align,
        flexWrap: wrapIt,
        flex: props.flex,
        margin: props.m,
        padding: props.p,
        height: props.h,
        width: props.w
      } as StyleValue
    "
  >
    <!-- <span class="name" v-if="props.name">
      {{ props.name }}
    </span> -->
    <slot />
  </component>
</template>

<style scoped>
.box {
  display: flex;
  position: relative;
  width: 100%;
  height: 100%;
  overflow: auto;
  border: 1px solid black;
}

/* .name {
  position: absolute;
  font-size: 90%;
  margin-top: -22px;
  text-shadow:
    -1px 0 white,
    0 1px white,
    1px 0 white,
    0 -1px white;
} */
</style>
