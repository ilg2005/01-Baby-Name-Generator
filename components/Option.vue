<script setup>
import {useState} from "nuxt/app";

const generator = useState('generatorState', () => ({gender: 'Boy', popularity: 'Trendy', length: 'Long'}));
defineProps(['option']);

const selectOption = (evt, optionType) => {
  if (evt.target.nodeName === 'BUTTON') {
    generator.value[optionType] = evt.target.innerText;
    const parent = evt.target.parentNode;
    const options = parent.querySelectorAll('.option');
    Array.from(options, option => option.classList.remove('option-active'));
    evt.target.classList.add('option-active');
  }
};

</script>

<template>
  <div class="option-container">
    <h4>{{ option.title }}</h4>
    <div class="option-buttons" @click="selectOption($event, option.type)">

      <button class="option"
              v-for="(btn, index) in option.btns"
              :key="btn"
              :class="{
                'option-left': index === 0,
                'option-right': index === option.btns.length - 1,
                'option-active': index === 0
               }"
      >
        {{ btn }}
      </button>
    </div>
  </div>

</template>

<style scoped>
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

</style>
