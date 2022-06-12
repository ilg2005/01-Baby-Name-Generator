<template>
  <div class="card">
    <h4>{{ name }}</h4>
    <p>x</p>
  </div>
</template>

<script setup>
defineProps(['name']);

</script>

<style scoped>
.card {
  background-color: rgb(27, 60, 138);
  width: 28%;
  color: white;
  border-radius: 1rem;
  padding: 0.1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  position: relative;
}
.card p {
  position: absolute;
  top: -20%;
  left: 92.5%;
  cursor: pointer;
  color: white;
}

</style>
