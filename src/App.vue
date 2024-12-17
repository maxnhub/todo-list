<template>
  <div id="app">
    <Header />
    <div class="container">
      <h1 class="title">TODO LIST</h1>
      <hr />
      <TodoInput @add-item="addItem" />
      <TodoTable
        :list="filteredList"
        @delete-item="deleteItem"
        @edit-item="editItem"
        @toggle-completed="toggleCompleted"
      />
    </div>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue';
import Header from './components/Header.vue';
import TodoInput from './components/TodoInput.vue';
import TodoTable from './components/TodoTable.vue';

// Reactive variables
const list = ref([]);
const searchInput = ref('');

// Computed property for filtered list
const filteredList = computed(() =>
  list.value.filter((item) =>
    item.value.toLowerCase().includes(searchInput.value.toLowerCase())
  )
);

// Methods
const addItem = (newItem) => {
  if (newItem.trim() !== '') {
    list.value.push({
      id: Math.random(),
      value: newItem.trim(),
      completed: false,
    });
  }
};

const deleteItem = (index) => {
  list.value.splice(index, 1);
};

const editItem = (index) => {
  const editedTodo = prompt('Edit the todo:');
  if (editedTodo !== null && editedTodo.trim() !== '') {
    list.value[index].value = editedTodo.trim();
  }
};

const toggleCompleted = (index) => {
  list.value[index].completed = !list.value[index].completed;
};
</script>
