<template>
    <div id="modal" class="modal hidden" ref="modal">
        <div class="modal-content">
        <h3>Edit Todo</h3>
        <input type="text" v-model="input" />
        <button @click="emitSave">Save</button>
        <button @click="emitClose">Cancel</button>
    </div>
</div>
</template>

<script setup>
import { ref } from 'vue';

// Локальные переменные
const input = ref('');
const modal = ref(null);

// Определяем события для взаимодействия с родительским компонентом
const emit = defineEmits(['save', 'close']);

// Показываем модальное окно
const show = (defaultValue) => {
  input.value = defaultValue;
  modal.value?.classList.remove('hidden');
};

// Закрываем модальное окно
const emitClose = () => {
  modal.value?.classList.add('hidden');
  input.value = '';
  emit('close');
};

// Сохраняем изменения и отправляем событие
const emitSave = () => {
  emit('save', input.value);
  emitClose();
};

// Экспортируем метод show для вызова из родительского компонента
defineExpose({
  show,
});
</script>

<style scoped>
.modal.hidden {
    display: none;
}
.modal {
    position: fixed;
    top: 50%;
    left: 50%;
    transform: translate(-50%, -50%);
    background: white;
    padding: 1rem;
    box-shadow: 0 2px 10px rgba(0, 0, 0, 0.1);
    }
</style>