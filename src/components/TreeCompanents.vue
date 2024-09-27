<template>
  <div>
    <button 
      @click="toggle" 
      class="w-full text-left bg-gray-200 p-3 mb-2  hover:bg-gray-300"
      :class="{ 'border-l-4 border-sky-500': isFocused }"  
      @focus="setFocus(true)" @blur="setFocus(false)"
    >
      <slot name="label" />
      <span :class="{'rotate-180': isOpen, 'text-sky-500': isFocused}" class="transition-transform float-right">▲</span>
    </button>
    <div v-if="isOpen" class="pl-4">
      <slot />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const props = defineProps({
  modelValue: Boolean,
})

const emit = defineEmits(['update:modelValue'])

const isOpen = ref(props.modelValue)
const isFocused = ref(false)

const toggle = () => {
  isOpen.value = !isOpen.value
  emit('update:modelValue', isOpen.value)
}

const setFocus = (value) => {
  isFocused.value = value
}

</script>

<style scoped>
.rotate-180 {
  transform: rotate(180deg);
  transition: transform 0.3s ease; 
}
</style>
