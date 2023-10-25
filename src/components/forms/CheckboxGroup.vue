<script setup lang="ts">
import { ref, onMounted } from 'vue'

const props = defineProps<Props>()
interface Props {
  data: any[]
  row?: string
  title?: string
}

const emit = defineEmits<{
  'update:modelValue': [value: object]
}>()

const optionsList = ref([])

onMounted(() => {
  props.data.map((item, index) => {
    let listItem = optionsList.value[index]

    let option = listItem.querySelector('input.option')
    let subOptions = listItem.querySelectorAll('input.subOption')

    option.onclick = function () {
      if (subOptions.length) {
        for (var i = 0; i < subOptions.length; i++) {
          subOptions[i].checked = this.checked
          item.children[i].checked = this.checked
        }
      }
    }

    if (subOptions.length) {
      for (let i = 0; i < subOptions.length; ++i) {
        console.log(subOptions[i])

        subOptions[i].onclick = function () {
          var checkedCount = listItem.querySelectorAll('input.subOption:checked').length

          option.checked = checkedCount > 0
          item.checked = checkedCount > 0

          option.indeterminate = checkedCount > 0 && checkedCount < subOptions.length
        }
      }
    }
  })
})
</script>

<template>
  <ul ref="ul">
    <li v-for="box in data" ref="optionsList">
      <label>
        <input v-model="box.checked" type="checkbox" class="option" />
        {{ box.label }}
      </label>
      <ul v-if="box.children">
        <li v-for="deepBox in box.children">
          <label>
            <input v-model="deepBox.checked" type="checkbox" class="subOption" />
            {{ deepBox.label }}
          </label>
        </li>
      </ul>
    </li>
  </ul>
</template>

<style scoped></style>
