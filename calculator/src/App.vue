<template>
    <div class="calculator">
        <div class="display">{{ displayValue }}</div>
        <div class="buttons">
            <NumberButtons v-for="number in numbers" :key="number" :number="number" @getNum="handleNumberClick(number)"></NumberButtons>
            <OperatorButtons v-for="operator in operators" :key="operator" @getOperator="handleOperatorClick(operator)" :operatorSign="operator"></OperatorButtons>
            <button class="operate-btns" @click="handleEqualClick">=</button>
            <button class="operate-btns" @click="handleClearClick">C</button>
      </div>
    </div>
</template>


<script setup>


import NumberButtons from './components/NumberButtons.vue';
 import { ref } from 'vue';
import OperatorButtons from './components/OperatorButtons.vue';

 const numbers = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9];
 const PLUS_OPERATOR = ref('+')
 const MINUS_OPERATOR = ref('-')
const MULTIPLE_OPERATOR = ref('*')
// const operators = [PLUS_OPERATOR,MINUS_OPERATOR,MULTIPLE_OPERATOR]
const operators = ['+','-','*']

const displayValue = ref('0');
const operator = ref(null);
const firstNumber = ref(null);

const handleNumberClick = (number) => {
    if (displayValue.value === '0') {
      displayValue.value = String(number);
    } else {
      displayValue.value += String(number);
    }
  };
  const resetOperations = ()=>{
    operator.value = null;
  }

  const resetDisplay =()=>{
    displayValue.value='0';
  }
  const resetFirstNumber = ()=>{
    firstNumber.value = null;
  }

  const handleOperatorClick = (op) => {
    operator.value = op;
    firstNumber.value = Number(displayValue.value);
    resetDisplay();
  };
  
  const handleEqualClick = () => {
    if (operator.value === PLUS_OPERATOR.value) {
      displayValue.value = String(firstNumber.value + Number(displayValue.value));
      
    }
    else if(operator.value === MULTIPLE_OPERATOR.value){
        displayValue.value = String(firstNumber.value * Number(displayValue.value));
    }
    else if(operator.value === MINUS_OPERATOR.value){
        displayValue.value = String(firstNumber.value - Number(displayValue.value));
    }
    resetOperations();
    resetFirstNumber();
  };
  
  const handleClearClick = () => {
    resetDisplay();
    resetOperations();
    resetFirstNumber();
  };

</script>

<style>
.calculator {
  width: 320px;
  margin: 0 auto;
  border: 1px solid #ccc;
  border-radius: 10px;
  padding: 15px;
  background: #daf103;
}

.display {
  font-size: 30px;
  text-align: right;
  padding: 8px;
  background-color: #36e1ff;
  border-radius: 8px;
  margin-bottom: 15px;
}

.buttons {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  grid-gap: 15px;
}

button {
  font-size: 20px;
  padding: 14px 20px;
  border: none;
  border-radius: 8px;
  background-color: #86ffaa;
  cursor: pointer;
  color: rgb(5, 5, 5);
}

button:hover {
  background-color: #e0e0e0;
}

button:active {
  background-color: #ccc;
}

.operate-btns{
  background: #ff3eb5;
}
</style>