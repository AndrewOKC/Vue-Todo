<script setup lang="ts">
import { ref } from "vue";

const newTask = ref("");
const error = ref("");

const emit = defineEmits<{
    formSubmitted: [newTask: string];
}>();

function formSubmitted() {
    if (newTask.value.trim()) {
        emit("formSubmitted", newTask.value.trim());
        newTask.value = "";
    } else {
        error.value = "Task cannot be empty!";
    }
}
</script>

<template>
    <form @submit.prevent="formSubmitted">
        <label>
            New Task
            <input v-model="newTask" name="newTask" :aria-invalid="!!error || undefined" @input="error = ''" />
            <small v-if="error" id="invalid-helper">
                {{ error }}
            </small>
        </label>
        <div class="button-container">
            <button>Add</button>
        </div>
    </form>
</template>

<style scoped>
.button-container {
    display: flex;
    justify-content: flex-end;
}
</style>
