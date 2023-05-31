<template>
    <form @submit.prevent="handleSubmit">
        <input type="text" placeholder="I need to..." v-model="newTask">
        <button>Add</button>
    </form>
</template>

<script>
import { ref } from 'vue';
import { useTaskStore } from '../stores/TaskStore';

export default {
    setup() {
        const taskStore = useTaskStore();

        const newTask = ref('');

        const handleSubmit = () => {
            if (newTask.value.length > 0) {
                taskStore.addTask({
                    title: newTask.value,
                    isFav: false,
                    id: Object.values(taskStore.tasks).pop().id + 1 // gets the last object's key and adds one to it to be the next in the object array
                });
                newTask.value = ''
            }
        }

        return { handleSubmit, newTask }
    }
}
</script>