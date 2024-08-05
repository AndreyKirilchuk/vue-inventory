<script setup>
import {onMounted, ref} from 'vue';

const thisTheme = ref('')

const setTheme = () => {
  document.body.removeAttribute('dark');
  document.body.removeAttribute('light');
  document.body.setAttribute(localStorage.getItem('theme'), '');
}

const toggleTheme = (event) => {
  localStorage.setItem('theme', event.target.value);
  setTheme()
}

onMounted(() => {
  setTheme()
  thisTheme.value = localStorage.getItem('theme')
});

</script>

<template>
  <select @change="toggleTheme">
    <option value="dark" :selected="thisTheme === 'dark' ? true : false">Темная тема</option>
    <option value="light" :selected="thisTheme === 'light' ? true : false">Светлая тема</option>
  </select>
</template>

<style scoped>
select{
  background: var(--var--elbackground);
  padding: 12px 14px;
  border-radius: 12px;
  border: 1px solid var(--var--elborder);
  color: var(--var--elcolor);
  width: 100%;
  outline: none;
  cursor: pointer;
  font-size: 14px;
  margin-top: 24px;
}


</style>