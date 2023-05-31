<template>
    <main>
        <!-- heading -->
        <header>
            <img src="./assets/pinia-logo.svg" alt="pinia logo">
            <h1>Pinia Tasks</h1>
        </header>

        <!-- new task form -->
        <div class="new-task-form">
            <TaskForm />
        </div>

        <!-- filter -->
        <nav class="filter">
            <button @click="filter = 'all'">All tasks</button>
            <button @click="filter = 'favs'">Fave tasks</button>
        </nav>

        <!-- loading -->
        <div class="loading" v-if="loading">Loading tasks...</div>

        <!-- task list -->
        <div class="task-list">
            <template v-if="filter === 'all'">
                <Tasks :tasks="tasks">
                    <p>You have {{ totalCount }} tasks left to do</p>
                </Tasks>
            </template>
            <template v-else-if="filter === 'favs'">
                <Tasks :tasks="favs">
                    <p>You have {{ favCount }} faves left to do</p>
                </Tasks>
            </template>
        </div>
    </main>
</template>

<script>
import { ref } from 'vue';
import Tasks from './components/Tasks.vue';
import { useTaskStore } from './stores/TaskStore'
import TaskForm from './components/TaskForm.vue';
import { storeToRefs } from 'pinia';

export default {
    components: { Tasks, TaskForm },

    setup() {
        const taskStore = useTaskStore();

        const { tasks, loading, favs, totalCount, favCount } = storeToRefs(taskStore)

        // fetch tasks
        taskStore.getTasks()

        const filter = ref('all')

        return { taskStore, filter, tasks, loading, favs, totalCount, favCount }
    }
}
</script>