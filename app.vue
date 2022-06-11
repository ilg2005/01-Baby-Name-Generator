<script setup>
import {names} from './names.js';

const selectedNames = ref();


const generator = reactive({gender: '', popularity: '', length: 'All'});

const selectOption = (evt, optionType) => {
  if (evt.target.nodeName === 'BUTTON') {
    generator[optionType] = evt.target.innerText;
    const parent = evt.target.parentNode;
    const options = parent.querySelectorAll('.option');
    Array.from(options, option => option.classList.remove('option-active'));
    evt.target.classList.add('option-active');
  }
};

const selectNames = () => selectedNames.value = names
    .filter(item => generator.gender === '' ? item : item.gender === generator.gender)
    .filter(item => generator.popularity === '' ? item : item.popularity === generator.popularity)
    .filter(item => generator.length === 'All' ? item : item.length === generator.length)
    .map(item => item.name);
</script>

<template>
  <div class="container">
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options-container">
      <div class="option-container">
        <h4>1) Choose a gender</h4>
        <div class="option-buttons" @click="selectOption($event, 'gender')">
          <button
              class="option option-left"
          >
            Boy
          </button>
          <button
              class="option"
          >
            Unisex
          </button>
          <button
              class="option option-right"
          >
            Girl
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>2) Choose the name's popularity</h4>
        <div class="option-buttons" @click="selectOption($event, 'popularity')">
          <button
              class="option option-left"
          >
            Trendy
          </button>
          <button
              class="option option-right"
          >
            Unique
          </button>
        </div>
      </div>
      <div class="option-container">
        <h4>3) Choose name's length</h4>
        <div class="option-buttons" @click="selectOption($event, 'length')">
          <button
              class="option option-left"
          >
            Long
          </button>
          <button
              class="option"
          >
            All
          </button>
          <button
              class="option option-right"
          >
            Short
          </button>
        </div>
      </div>
      <button class="primary" @click="selectNames">Find Names</button>
    </div>
    {{ selectedNames }}
  </div>
</template>

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

.option-container {
  margin-bottom: 2rem;
}

.option {
  background: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
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

</style>
