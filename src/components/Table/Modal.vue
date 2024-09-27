<template>
    <transition name="modal">
      <div class="modal" v-if="isVisible">
        <div class="modal-overlay" @click="closeModal"></div>
        <div class="modal-content">
          <slot></slot>
          
          <button @click="closeModal" class="bg-red-500 mt-3 text-white px-[4px] py-[2px] rounded ml-2">Yopish</button>
        </div>
      </div>
    </transition>
  </template>
  
  <script setup>
  import { defineProps, ref } from 'vue';
  
  const props = defineProps({
    isVisible: {
      type: Boolean,
      required: true
    },
    close: {
      type: Function,
      required: true
    }
  });
  
  function closeModal() {
    props.close();
  }
  </script>
  
  <style>
  .modal {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
  }
  
  .modal-overlay {
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
  }
  
  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 8px;
    position: relative;
    z-index: 10;
  }
  </style>
  