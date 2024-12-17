<template>
    <div class="todo-table">
        <div class="table-header">
            <div class="table-cell">Task</div>
            <div class="table-cell">Actions</div>
        </div>
        <div class="table-body">
            <div class="table-row" v-for="(item, index) in list" :key="item.id"
                :class="{ 'even-row': index % 2 === 0, completed: item.completed }">
                <div class="table-cell" :class="{ 'completed-cell': item.completed }">
                    {{ item.value }}
                </div>
                <div class="table-cell">
                    <button class="btn btn-primary" @click="() => $emit('toggle-completed', index)">
                        {{ item.completed ? 'Undo' : 'Complete' }}
                    </button>
                    <button class="btn btn-info" @click="() => $emit('edit-item', index)">
                        Edit
                    </button>
                    <button class="btn btn-danger" @click="() => $emit('delete-item', index)">
                        Delete
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

// Props
defineProps({
    list: {
        type: Array,
        required: true,
    },
});

// Emits
defineEmits(['delete-item', 'edit-item', 'toggle-completed']);
</script>