<template>
    <div :key="task.id" v-for="task in tasks">
        <TaskSingle @delete-task="$emit('delete-task',task.id)" :task="task"/>
    </div>

</template>

<script>
import TaskSingle from './TaskSingle.vue'

export default {
    name: 'Tasks-one',
    props: {
        tasks: {
            type: Array
        }
    },
    components: {
        TaskSingle
    },
    emits: ['delete-task'],
}

</script>
