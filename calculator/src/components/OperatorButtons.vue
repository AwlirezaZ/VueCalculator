<template>
    <div>
        <button class="operate-btns" @click="emit('getOperator')">{{ operatorSign }}</button>
    </div>
</template>

<script setup>

import { defineProps } from 'vue';
defineProps({
    operatorSign:String
})
const emit = defineEmits([
  'getOperator'
])

</script>

<style>
.operate-btns{
  background: #ff3eb5;
}</style>
