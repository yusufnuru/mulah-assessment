<script setup lang="ts">
import { ref } from 'vue'
import TableOne from '@/components/TableOne.vue'
import TableTwo from '@/components/TableTwo.vue'
import type { TableOneData } from '@/types.ts'

const tableOneData = ref<TableOneData[]>([])
const handleLoaded = (data: TableOneData[]) => {
  tableOneData.value = data
}
</script>

<template>
  <div class="mx-auto p-4">
    <h1 class="text-primary text-2xl font-extrabold">Mulah Table Output and Processing Assessment </h1>
  <div class="w-full mx-auto p-4 sm:flex">
    <TableOne
      class="w-full mx-auto p-4"
      @loaded="handleLoaded"
    />
    <TableTwo
      class="w-full mx-auto p-4"
      :table-one-data="tableOneData" ref="tableOne"
    />
  </div>
    <footer class="mx-auto p-2 text-center">
      <p class="text-sm text-gray-500">© 2025 - Made by <a href="https://github.com/yusufnuru" class="text-blue-600 hover:underline">Yusuf Nuru</a></p>    </footer>
  </div>
</template>

