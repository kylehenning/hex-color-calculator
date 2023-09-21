

<script setup>
import { ref } from 'vue';

  let color1 = ref('F5678E');
  let color2 = ref('724BE2');
  let color3 = ref('FFFFFF');
  let color4 = ref('FFFFFF')
  let operator = ref('multiply')

  const handleInput1 = (e) => {
    color1.value = e.target.value;
  }
  const handleInput2 = (e) => {
    color2.value = e.target.value;
  }

  const changeHex = () => {
    let num1 = parseInt(color1.value, 16)
    let num2 = parseInt(color2.value, 16)
    let solution;
    switch (operator.value) {
      case 'multiply':
        solution = num1 * num2;
        break;
      case 'add':
        solution = num1 + num2;
        break;
      case 'subtract':
        solution = num1 - num2;
        break;
      case 'divide':
        solution = num1 / num2;
        break;
    }
    let fakeMod = parseInt('FFFFFF', 16);

    solution = solution % fakeMod;
    color3.value = solution.toString(16);
    console.log("Kyle's solution: ", color3.value)
  }

  const juliasWay = () => {
    let hex1Array = color1.value.match(/.{2}/g);
    let hex2Array = color2.value.match(/.{2}/g);
    let productsArray = [];
    let final= "";
    for (var i = 0; i < 3; i++) {
      switch (operator.value) {
      case 'multiply':
        productsArray.push((parseInt(hex1Array[i], 16) * parseInt(hex2Array[i], 16)) % 255);
        break;
      case 'add':
        productsArray.push((parseInt(hex1Array[i], 16) + parseInt(hex2Array[i], 16)) % 255);
        break;
      case 'subtract':
        productsArray.push((parseInt(hex1Array[i], 16) - parseInt(hex2Array[i], 16)) % 255);
        break;
      case 'divide':
        productsArray.push((parseInt(hex1Array[i], 16) / parseInt(hex2Array[i], 16)) % 255);
        break
    }
      productsArray[i] = productsArray[i].toString(16);
      final = final + productsArray[i];
    }
    console.log("Julia's solution: ", final)
    color4.value = final;

  }

</script>

<template>

  <div class="flex items-center m-10 flex-col">
    <h1 class=" text-4xl">Hex Color Calculator</h1>
    <div class="flex flex-row w-1/2 m-20 justify-between">
      <input type="text" @input="handleInput1" class=" bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-1/3 p-2.5" :value="color1" />
      <div :style="{'background-color': '#' + color1}" class=" w-1/4 border border-black" ></div>
    </div>
    <div class="flex flex-row w-1/2 m-20 justify-between">
      <input type="text" @input="handleInput2" class=" bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-1/3 p-2.5" :value="color2" />
      <div :style="{'background-color': '#' + color2}" class=" w-1/4 border border-black" ></div>
    </div>
    <label for="countries" class="block mb-2 text-sm font-medium text-gray-900 dark:text-white">Select an option</label>
    <select id="countries" v-model="operator" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-1/2 p-2.5">
      <option selected>Choose an operation</option>
      <option value="multiply">Multiplication</option>
      <option value="add">Addition</option>
      <option value="subtract">Subtract</option>
      <option value="divide">Divide</option>
    </select>
    <div class="flex flex-row w-1/2 m-20 justify-between">
      <button @click="changeHex" class="bg-blue-400 w-24 p-5 rounded">Try it</button>
      <div :style="{'background-color': '#' + color3}" class=" w-1/4 border border-black" ></div>
    </div>
    <div class="flex flex-row w-1/2 m-20 justify-between">
      <button @click="juliasWay" class="bg-blue-400 w-24 p-5 rounded">JULIAS WAY</button>
      <div :style="{'background-color': '#' + color4}" class=" w-1/4 border border-black" ></div>
    </div>
    

  </div>
</template>
