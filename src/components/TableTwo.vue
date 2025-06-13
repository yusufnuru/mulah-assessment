<script setup lang="ts">
import { ref, watch } from 'vue'
import type { TableOneData, TableTwoData } from '@/types.ts'

const props = defineProps({
  tableOneData: {
    type: Array as () => TableOneData[],
    required: true,
  },
})

const tableTwoData = ref(<TableTwoData[]>[]);
const getValue = (label: string) :number => {
  const found = props.tableOneData.find(row => row.label === label)
  if (found) {
    return found.value
  } else {
    console.warn(`Label "${label}" not found in table data.`)
    return 0
  }
}

watch(() => props.tableOneData, (newTable) => {
  if (newTable?.length > 0) {
    tableTwoData.value = [
      { category: 'Alpha', value: getValue('A5') + getValue('A20') },
      { category: 'Beta', value: Math.floor(getValue('A15') / getValue('A7')) },
      { category: 'Charlie', value: getValue('A13') * getValue('A12') },
    ]
  }
}, { immediate: true })
</script>

<template>
  <div >
    <h2 class="text-xl text-primary font-extrabold">Table 2</h2>
    <table border="1" cellspacing="0" cellpadding="8" class="w-full">
      <thead >
      <tr>
        <th>Category</th>
        <th>Value</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="row in tableTwoData" :key="row.category">
        <td>{{ row.category }}</td>
        <td>{{ row.value }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

<style scoped>

</style>
