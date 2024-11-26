<script setup>
import { computed } from "vue";

const props = defineProps({
  salaries: Array
});

const emit = defineEmits();

const removeSalary = (id) => {
    emit('remove-salary', id);
};

const totalAmount = computed(() => {
    return props.salaries.reduce((sum, salary) => sum + parseFloat(salary.salary), 0).toFixed(2);
});

const totalAmountAfterTax = computed(() => {
    return props.salaries.reduce((sum, salary) => sum + parseFloat(salary.salary) * 0.85, 0).toFixed(2);
});
</script>

<template>
  <table class="table">
    <thead>
      <tr>
        <th>#</th>
        <th>ФИО</th>
        <th>Дата выдачи</th>
        <th>Отработанные дни</th>
        <th>Сумма без налогов</th>
        <th>Сумма с налогами</th>
        <th>Действие</th>
      </tr>
    </thead>
    <tbody>
      <tr v-for="(salary, index) in salaries" :key="salary.id">
        <td>{{ index + 1 }}</td>
        <td>{{ salary.name }}</td>
        <td>{{ salary.date }}</td>
        <td>{{ salary.days }}</td>
        <td>{{ salary.salary }}</td>
        <td>{{ (salary.salary * 0.85).toFixed(2) }}</td>
        <td><button @click="removeSalary(salary.id)" class="btn btn-danger">Удалить</button></td>
      </tr>
    </tbody>
  </table>
  <div class="mt-3">
    <h5>Общая сумма (без налогов): ${{ totalAmount }}</h5>
    <h5>Общая сумма (с налогами): ${{ totalAmountAfterTax }}</h5>
  </div>
</template>
