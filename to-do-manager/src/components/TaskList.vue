<script setup lang="ts">
import { defineProps } from 'vue';
import { defineEmits } from 'vue';
interface Task {
  id: number;
  title: string;
  completed: boolean;
}

const tasks=defineProps<{
    tasks:Task[],

}>();
const emit=defineEmits<{
    (event: 'toggleCompletion', payload: number): void;
  (event: 'delete-task', payload: number): void;
}>();
const toggleCompletion=(taskId:number)=>{
    emit('toggleCompletion',taskId);

}
const deleteTask = (taskId: number) => {
  emit('delete-task', taskId); // Emit the event to the parent component
};

</script>
<template>

    <ul>
        <li v-for="(task,index) in $props.tasks" :key="task.id">{{ task.title }}
            <button @click="toggleCompletion(task.id)">
            {{ task.completed ? 'Undo' : 'Complete' }}
            </button>
            <button @click="deleteTask(task.id)">Delete</button>
        </li>
    </ul>
    
</template>