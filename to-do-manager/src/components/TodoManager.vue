<script setup lang="ts">
import { ref } from 'vue';
import TaskList from './TaskList.vue';
interface Task{
    id:number,
    title:string,
    completed:boolean;
}
const newTaskTitle=ref('')
const tasks=ref<Task[]>(
    [
        {id:1,title:'task 1',completed:false}
    ]
);

const addTask=(title:string)=>{
    const newTask={
        id:tasks.value.length+1,
        title,
        completed:false,

    }
    tasks.value.push(newTask)

}

const deleteTask=(id:number)=>{
    tasks.value=tasks.value.filter(task=>task.id !==id)
}

const handleToggleCompletion=((taskId:number)=>{
    const task=tasks.value.find((task)=>task.id===taskId);
    if(task){
        task.completed=!task.completed;
    }
})


</script>

<template>

    <TaskList :tasks="tasks" @toggleCompletion="handleToggleCompletion" @delete-task="deleteTask"></TaskList>
    <input v-model="newTaskTitle" placeholder="enter a task">
    <button @click="addTask(newTaskTitle)">Add</button>
</template>