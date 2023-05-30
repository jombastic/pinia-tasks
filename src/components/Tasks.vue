<template>
    <slot></slot>
    <div v-for="task in tasks" :key="task.id">
        <TaskDetails :task="task" />
    </div>
</template>

<script>
import TaskDetails from './TaskDetails.vue'
export default {
    components: { TaskDetails },
    props: ['tasks']
}
</script>