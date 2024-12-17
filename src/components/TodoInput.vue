<template>
    <div class="input-group">
        <input type="text" class="form-control" placeholder="Add item..." v-model="input" @keyup.enter="emitAddItem" />
        <button class="btn btn-success" @click="emitAddItem">ADD</button>
    </div>
</template>

<script setup>
import { ref, defineEmits } from 'vue';

// Define emitted events
const emit = defineEmits(['add-item']);

// Reactive input state
const input = ref('');

// Emit add-item event
const emitAddItem = () => {
    console.log('Emitting add-item:');
    if (input.value.trim() !== '') {
        emit('add-item', input.value);
        console.log('Emitting add-item with value:');
        input.value = '';
    }
};
</script>