<script setup lang="ts">
import { computed } from 'vue'

type TableHeaders = {
  key: string
  name: string
}

const props = defineProps<Props>()
interface Props {
  data?: object
  tableHeaders?: TableHeaders[]
}

function digForValue(row: any, keys: string[]): string {
  if (keys.length > 1) {
    return digForValue(row[keys.shift()!], keys)
  } else {
    return row[keys[0]]
  }
}
</script>

<template>
  <table style="text-align: left">
    <tr>
      <th v-for="{ name } in props.tableHeaders">{{ name }}</th>
    </tr>
    <tr v-for="row in data" draggable="false" :ondragstart="() => {}" :ondragover="() => {}">
      <td v-for="{ key } in props.tableHeaders">{{ digForValue(row, key.split('.')) }}</td>
    </tr>
  </table>
</template>

<style scoped></style>
