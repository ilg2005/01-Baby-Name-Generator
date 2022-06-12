<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options-container">
      <Option v-for="optionItem in optionsArray"
              :key="optionItem.title"
              :option="optionItem"
      />
      <button class="primary" @click="selectNames">Find Names</button>
    </div>
    <div class="cards-container">
      <Card v-for="name in selectedNames" :key="name" :name="name"/>
    </div>
  </div>
</template>

<script setup>
import {names} from './names.js';
import {useState} from "nuxt/app";

const selectedNames = ref();
const generator = useState('generatorState');

const optionsArray = [
  {
    title: '1) Choose a gender',
    type: 'gender',
    btns: ['Boy', 'Unisex', 'Girl']
  },
  {
    title: "2) Choose the name's popularity",
    type: 'popularity',
    btns: ['Trendy', 'Unique']
  },
  {
    title: "3) Choose name's length",
    type: 'length',
    btns: ['Long', 'All', 'Short']
  },
];

const selectNames = () => selectedNames.value = names
    .filter(item => item.gender === generator.value.gender)
    .filter(item => item.popularity === generator.value.popularity)
    .filter(item => generator.value.length === 'All' ? item : item.length === generator.value.length)
    .map(item => item.name);
</script>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin: 1rem auto;
  cursor: pointer;
}
.cards-container {
  display: flex;
  margin: 3rem auto;
  flex-wrap: wrap;
}
</style>
