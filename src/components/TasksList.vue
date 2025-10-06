<script setup lang="ts">
import type { Task } from "../types";

const props = defineProps<{
    tasks: Task[];
}>();

const emits = defineEmits<{
    checkboxChecked: [id: string];
}>();
</script>

<template>
    <article v-for="task in props.tasks" :key="task.id">
        <label>
            <input @input="emits('checkboxChecked', task.id)" :checked="task.completed" type="checkbox" />
            {{ task.title }}
        </label>
    </article>
</template>
