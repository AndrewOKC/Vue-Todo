<script setup lang="ts">
import { ref } from "vue";
import TodoForm from "./components/TodoForm.vue";
import type { Task } from "./types";

const message = ref("My Todo List");
const tasks = ref<Task[]>([]);

function addTask(newTask: string) {
    tasks.value.push({
        id: crypto.randomUUID(),
        title: newTask,
        completed: false,
    });
}
</script>

<template>
    <main>
        <h1>{{ message }}</h1>
        <!-- When the form component emits the addTask event, it will call the addTask function in this component -->
        <TodoForm @addTask="addTask" />
        <h3>There are {{ tasks.length }} tasks.</h3>
        <article v-for="task in tasks" :key="task.id">
            {{ task.title }}
        </article>
    </main>
</template>

<style>
main {
    max-width: 800px;
    margin: 1rem auto;
}
.button-container {
    display: flex;
    justify-content: flex-end;
}
</style>
