<template>
    <div class="overflow-x-auto">
      <table class="min-w-full bg-white shadow-md rounded-lg overflow-hidden">
        <thead class="bg-gray-800 text-white">
          <tr>
            <th
              v-for="(header, index) in headers"
              :key="index"
              class="py-3 px-4 text-left text-sm font-semibold border-b border-gray-300"
            >
              {{ header }}
            </th>
          </tr>
        </thead>
        <tbody>
          <tr
            v-for="(row, rowIndex) in data"
            :key="rowIndex"
            class="hover:bg-gray-100 transition duration-200"
          >
            <td
              v-for="(item, colIndex) in row"
              :key="colIndex"
              class="py-3 px-4 border-b border-gray-300 text-sm text-gray-700"
            >
              {{ item }}
            </td>
          </tr>
        </tbody>
      </table>
    </div>
  </template>
  
  <script setup>
  import { defineProps } from "vue";
  
  const props = defineProps({
    headers: {
      type: Array,
      required: true,
    },
    data: {
      type: Array,
      required: true,
    },
  });
  </script>
  
  <style scoped>
  table {
    border-collapse: collapse;
  }
  </style>
  