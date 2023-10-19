<script setup lang="ts">
import { computed, onMounted, ref, type Ref, type StyleValue, type VNode } from 'vue'

const props = defineProps<Props>()
interface Props {
  h?: string
  w?: string
  m?: string
  mt?: string
  mb?: string
  mr?: string
  ml?: string
  p?: string
  pt?: string
  pb?: string
  pr?: string
  pl?: string
  row?: boolean
  reverse?: boolean
  wrap?: boolean
  justify?: 'center' | 'flex-start' | 'flex-end' | 'space-between' | 'space-around' | 'space-evenly'
  align?: 'center' | 'flex-start' | 'flex-end'
  flex?: string
  as?: 'header' | 'footer' | 'main' | 'article' | 'section' | 'aside'
  name?: string
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
let counter = 0

//
const getParentBoxesCount: any = (el: HTMLElement) => {
  if (el.parentElement!.tagName === 'BODY') {
    return `_${counter}`
  } else if (el.classList.contains('box')) {
    counter++
    return getParentBoxesCount(el.parentElement)
  } else {
    return getParentBoxesCount(el.parentElement)
  }
}

const box = ref()
const colorfull = ref('')

const enableColorful = () => {
  const boxLevelColors = {
    _1: '#6876FC',
    _2: '#38BDF8',
    _3: '#01B598',
    _4: '#99DA2F',
    _5: '#FBBF24',
    _6: '#FB923D',
    _7: '#F472B6',
    _8: '#C084FC',
    _9: '#9A1799',
    _10: '#595959'
  }
  colorfull.value = boxLevelColors[getParentBoxesCount(box.value) as keyof typeof boxLevelColors]
}

onMounted(() => {
  enableColorful()
})
</script>

<template>
  <component
    ref="box"
    :is="renderAs"
    class="box"
    :style="
      {
        borderColor: colorfull ? colorfull : 'transparent',
        flexDirection: direction,
        justifyContent: props.justify,
        alignItems: props.align,
        flexWrap: wrapIt,
        flex: props.flex,
        margin: props.m && props.m,
        marginTop: !props.mt ? props.m : props.mt,
        marginBottom: !props.mb ? props.m : props.mb,
        marginRight: !props.mr ? props.m : props.mr,
        marginLeft: !props.ml ? props.m : props.ml,
        padding: props.p,
        paddingTop: !props.pt ? props.p : props.pt,
        paddingBottom: !props.pb ? props.p : props.pb,
        paddingRight: !props.pr ? props.p : props.pr,
        paddingLeft: !props.pl ? props.p : props.pl,
        maxHeight: props.h,
        maxWidth: props.w
      } as StyleValue
    "
  >
    <span v-if="props.name && colorfull" :style="{ color: colorfull }" class="name">
      {{ props.name }}
    </span>
    <slot />
  </component>
</template>

<style scoped>
.box {
  display: flex;
  position: relative;
  overflow: auto;
  border: 2px solid black;
  box-sizing: border-box;
  margin: 1rem;
  min-height: 24px;
}

.name {
  position: absolute;
  font-size: 80%;
  font-weight: 00;
  bottom: 0;
  right: 0;
  padding: 0 4px 0 4px;
  background: white;
}
</style>
