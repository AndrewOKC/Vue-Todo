<script setup lang="ts">
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import type { Task } from "./types";
import TasksList from "./components/TasksList.vue";

const message = ref("My Todo List");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
    tasks.value.push({
        id: crypto.randomUUID(),
        title: newTask,
        completed: false,
    });
}

function markComplete(id: string) {
    const task = tasks.value.find((task) => task.id === id);
    if (task) {
        task.completed = !task.completed;
    }
}
</script>

<template>
    <main>
        <h1>{{ message }}</h1>
        <!-- When the form component emits the addTask event, it will call the addTask function in this component -->
        <TodoForm @formSubmitted="addTask" />
        <h3 v-if="!tasks.length">Add a task to get started!</h3>
        <h3 v-else>0 / {{ tasks.length }} tasks completed</h3>
        <TasksList :tasks @checkboxChecked="markComplete" />
    </main>
</template>

<style>
main {
    max-width: 800px;
    margin: 1rem auto;
}
</style>
