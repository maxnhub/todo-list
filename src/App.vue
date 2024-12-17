<template>
  <div id="app">
    <Header />
    <div class="container">
      <h1 class="title">TODO LIST</h1>
      <hr />
      <TodoInput @add-item="addItem" />
      <TodoTable
        :list="list"
        @delete-item="deleteItem"
        @edit-item="editItem"
        @toggle-completed="toggleCompleted"
      />
      <Modal ref="modalRef" @save="handleSave" @close="handleClose" />
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import Header from './components/Header.vue';
import TodoInput from './components/TodoInput.vue';
import TodoTable from './components/TodoTable.vue';
import Modal from './components/Modal.vue';

// Список задач (реактивный)
const list = ref([]);
const modalRef = ref(null); // Ссылка на модальное окно
let editingIndex = null; // Индекс редактируемого элемента

// Добавляем задачу
const addItem = (newItem) => {
  if (newItem.trim() !== '') {
    list.value.push({
      id: Math.random(),
      value: newItem.trim(),
      completed: false,
    });
  }
};

// Удаляем задачу
const deleteItem = (index) => {
  list.value.splice(index, 1);
};

// Редактируем задачу
const editItem = (index) => {
  editingIndex = index;
  const currentTodo = list.value[index].value;
  modalRef.value.show(currentTodo); // Показываем модальное окно с текущим значением
};

// Обрабатываем сохранение из модального окна
const handleSave = (editedTodo) => {
  if (editingIndex !== null && editedTodo.trim() !== '') {
    // Обновляем задачу напрямую
    list.value[editingIndex].value = editedTodo.trim();
    editingIndex = null; // Сбрасываем индекс
  }
};

// Отмечаем задачу выполненной
const toggleCompleted = (index) => {
  list.value[index].completed = !list.value[index].completed;
};

// Обработка закрытия модального окна
const handleClose = () => {
  editingIndex = null;
};
</script>