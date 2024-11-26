<script setup>
import { ref } from "vue";

const name = ref('');
const date = ref('');
const days = ref(1);
const salary = ref(0);

const emit = defineEmits();

const addSalary = () => {
    if (name.value && date.value && days.value && salary.value) {
        emit('add-salary', {
            id: Date.now(),
            name: name.value,
            date: new Date(date.value).toLocaleDateString(),
            days: days.value,
            salary: salary.value
        });

        name.value = '';
        date.value = '';
        days.value = 1;
        salary.value = 0;
    } else {
        alert('Пожалуйста, заполните все поля.');
    }
};
</script>

<template>
  <form @submit.prevent="addSalary">
    <div class="mb-3">
      <label for="name" class="form-label">ФИО</label>
      <input type="text" v-model="name" class="form-control" id="name" required>
    </div>
    <div class="mb-3">
      <label for="date" class="form-label">Дата выдачи зарплаты</label>
      <input type="date" v-model="date" class="form-control" id="date" required>
    </div>
    <div class="mb-3">
      <label for="days" class="form-label">Количество отработанных дней</label>
      <input type="number" v-model="days" class="form-control" id="days" required>
    </div>
    <div class="mb-3">
      <label for="salary" class="form-label">Размер заработной платы</label>
      <input type="number" v-model="salary" class="form-control" id="salary" required>
    </div>
    <div class="text-center mb-3">
      <button type="submit" class="btn btn-dark">Добавить</button>
    </div>
  </form>
</template>
