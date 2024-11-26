<script setup>
import { ref } from "vue";
import Form from './components/Form.vue';
import List from './components/List.vue';

const salaries = ref([
    { id: 1, name: 'Иван Иванов', date: '20.11.2024', days: 20, salary: 1000 },
    { id: 2, name: 'Петр Петров', date: '25.11.2024', days: 22, salary: 1100 },
]);

const addSalary = (salary) => {
    salaries.value.push(salary);
};

const removeSalary = (id) => {
    salaries.value = salaries.value.filter(salary => salary.id !== id);
};
</script>

<template>
  <div class="container mt-5">
    <Form @add-salary="addSalary" />
    <List :salaries="salaries" @remove-salary="removeSalary" />
  </div>
</template>
