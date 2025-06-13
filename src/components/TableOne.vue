<script setup lang="ts">
import Papa, { type ParseResult } from 'papaparse'
import { onMounted, ref } from 'vue'
import type { TableOneData } from '@/types.ts'


const tableOneData = ref<TableOneData[]>([])
const tableHeaders = ref<string[]>([])
const emit = defineEmits<{
  (event: 'loaded', data: TableOneData[]): void
}>()

onMounted(() => {
  fetch('/data/Table_Input.csv')
    .then((res) => res.text())
    .then((csv) =>
      Papa.parse(csv, {
        header: true,
        skipEmptyLines: true,
        complete: (results: ParseResult<Record<string, string>>) => {
          const data = results.data
          if (!data.length) {
            console.error('No data found')
            return
          }

          const keys = Object.keys(data[0])
          tableHeaders.value = keys;
          if (keys.length < 2) {
            console.error('CSV must have at least two columns')
            return
          }

          const [labelKey, valueKey] = keys;

          tableOneData.value = data.map((row) => {
            return {
              label: row[labelKey],
              value: Number(row[valueKey]),
            };
          });
          emit('loaded', tableOneData.value)
        },
      }),
    )
})
</script>

<template>
  <div>
    <h2 class="text-xl text-primary font-extrabold">Table 1</h2>
    <table border="1" cellspacing="0" cellpadding="8" class="w-full">
      <thead>
      <tr>
        <th v-for="header in tableHeaders" :key="header">{{ header }}</th>
      </tr>
      </thead>
      <tbody>
      <tr v-for="row in tableOneData" :key="row.label">
        <td>{{ row.label }}</td>
        <td>{{ row.value }}</td>
      </tr>
      </tbody>
    </table>
  </div>
</template>

