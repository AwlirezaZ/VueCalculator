<template>
      <div>
          <button @click="emit('getNum')">{{ number }}</button>
      </div>
</template>

  <script setup>

  import { defineProps } from 'vue';
  defineProps({
    number:Number
  })
  const emit = defineEmits([
    'getNum'
  ])

  </script>
  

