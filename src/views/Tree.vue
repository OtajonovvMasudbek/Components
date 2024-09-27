<template>
    <div class="w-full max-w-xs mx-auto">
      <CollapsibleButton v-model="openSections.models" @focus="setFocus('models')" @blur="setFocus(null)">
        <template #label>
          Models
        </template>
        <CollapsibleButton v-model="openSections.dataWarehouse" @focus="setFocus('dataWarehouse')" @blur="setFocus(null)">
          <template #label>
            Data warehouse
          </template>
          <template #default>
            <p v-for="report in reports" :key="report.id" class="p-2 hover:bg-gray-100 cursor-pointer">{{ report.name }}</p>
          </template>
        </CollapsibleButton>
        <CollapsibleButton v-model="openSections.dataWarehouse" @focus="setFocus('dataWarehouse')" @blur="setFocus(null)">
          <template #label>
            Data warehouse
          </template>
          <template #default>
            <p v-for="report in reports" :key="report.id" class="p-2 hover:bg-gray-100 cursor-pointer">{{ report.name }}</p>
          </template>
        </CollapsibleButton>
      </CollapsibleButton>
  
      <CollapsibleButton v-model="openSections.statistics" @focus="setFocus('statistics')" @blur="setFocus(null)">
        <template #label>
          Statistics
        </template>
        <template #default>
          <p v-for="stat in statistics" :key="stat.id" class="p-2 hover:bg-gray-100 cursor-pointer">{{ stat.name }}</p>
        </template>
      </CollapsibleButton>
    </div>
  </template>
  
  <script setup>
  import { reactive, ref, onMounted } from 'vue'
  import axios from 'axios'
  import CollapsibleButton from '../components/TreeCompanents.vue'
  
  const openSections = reactive({
    models: false,
    dataWarehouse: false,
    statistics: false
  })
  
  const isFocusedSection = ref(null)
  const reports = ref([])
  const statistics = ref([])
  
  const setFocus = (section) => {
    isFocusedSection.value = section
  }
  
  const fetchReports = async () => {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/posts'); 
      reports.value = response.data.slice(0, 7).map(item => ({ id: item.id, name: item.title })); 
    } catch (error) {
      console.error('Error fetching reports:', error)
    }
  }
  
  const fetchStatistics = async () => {
    try {
      const response = await axios.get('https://jsonplaceholder.typicode.com/comments');
      statistics.value = response.data.slice(0, 5).map(item => ({ id: item.id, name: item.body }));
    } catch (error) {
      console.error('Error fetching statistics:', error)
    }
  }
  
  onMounted(() => {
    fetchReports()
    fetchStatistics()
  })
  </script>
  
  <style scoped>
  .float-right {
    float: right;
  }
  </style>
  