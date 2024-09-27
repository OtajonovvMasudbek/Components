<template>
    <div class="p-4">
      <Table :headers="tableHeaders" :data="tableData" :removeRow="removeRow" />
      <div class="mt-4">
        <button @click="showModal = true" class="bg-blue-500 text-white px-[10px] py-[4px] rounded font-bold flex items-center">
            Yangi qator qo'shish
        </button>
      </div>
  
      <Modal :isVisible="showModal" :close="() => (showModal = false)">
        <h2 class="text-lg font-bold">Yangi Qator Qo'shish</h2>
        <form @submit.prevent="addRow">
          <input v-model="newName" placeholder="Ism" required class="border outline-none p-1 m-1" />
          <input v-model="newAge" type="number" placeholder="Yosh" required class="border p-1 m-1" min="18" max="30" />
          <select v-model="newProvince" @change="fetchDistricts" required class="border p-1 m-1">
            <option disabled value="">Viloyat tanlang</option>
            <option v-for="province in provinces" :key="province" :value="province">{{ province }}</option>
          </select>
          <input v-model="newCity" placeholder="Shahar" required class="border p-1 m-1" />
          <input v-model="newDistrict" placeholder="Tuman" required class="border p-1 m-1" />
          <select v-model="employmentStatus" class="border p-1 m-1">
            <option value="Ishli">Ishli</option>
            <option value="Ishsiz">Ishsiz</option>
          </select>
          <button type="submit" class="bg-blue-500 text-white p-2 rounded">Qo'shish</button>
        </form>
      </Modal>
    </div>
  </template>
  
  <script setup>
  import { ref } from 'vue';
  import Table from '../components/Table/TableCompanent.vue';
  import Modal from '../components/Table/Modal.vue';
  
  const tableHeaders = ['Ism', 'Yosh', 'Shahar', 'Tuman', 'Viloyat', 'Ish'];
  
  const tableData = ref([
    ['Ali', 25, 'Toshkent', 'Yunusobod', 'Toshkent viloyati', 'Ishli'],
    ['Vali', 30, 'Samarqand', 'Samarqand', 'Samarqand viloyati', 'Ishsiz'],
  ]);
  
  const newName = ref('');
  const newAge = ref(null);
  const newCity = ref('');
  const newDistrict = ref('');
  const newProvince = ref('');
  const employmentStatus = ref('Ishsiz');
  const showModal = ref(false);
  const provinces = ['Toshkent', 'Samarqand', 'Buxoro', 'Andijon', 'Farg‘ona', 'Nukus', 'Urganch', 'Namangan', 'Xorazm', 'Jizzax', 'Sirdaryo', 'Qoraqalpog‘iston'];
  const districts = [];
  
  const addRow = () => {
    if (newName.value && newAge.value && newCity.value && newDistrict.value && newProvince.value) {
      tableData.value.push([newName.value, newAge.value, newCity.value, newDistrict.value, newProvince.value, employmentStatus.value]);
      resetForm();
      showModal.value = false;
    }
  };
  
  const removeRow = (index) => {
    tableData.value.splice(index, 1);
  };
  
  const resetForm = () => {
    newName.value = '';
    newAge.value = null;
    newCity.value = '';
    newDistrict.value = '';
    newProvince.value = '';
    employmentStatus.value = 'Ishsiz';
  };
  
  const fetchDistricts = () => {
    districts.value = getDistrictsByProvince(newProvince.value);
  };
  
  const getDistrictsByProvince = (province) => {
    const districtData = {
      Toshkent: ['Yunusobod', 'Chilonzor', 'Mirzo Ulugbek'],
      Samarqand: ['Samarqand', 'Kattaqo’rg’on', 'Jomboy'],
      Fargona: ['Farg‘ona', 'Quva', 'O’ztuqay'],
    };
    return districtData[province] || [];
  };
  </script>
  