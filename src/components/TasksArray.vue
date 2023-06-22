<template>
  <div>
    <TaskSingle
        v-for="task in tasks"
        :key="task.id"
        @delete-task="$emit('delete-task', task.id)"
        @updateWeather="$emit('updateWeather', task)"
        :task="task"
    />
  </div>
</template>

<script>
import TaskSingle from './TaskSingle.vue';

export default {
  name: 'TaskArray',
  props: {
    tasks: {
      type: Array
    }
  },
  components: {
    TaskSingle
  },
  emits: ['delete-task', 'updateWeather']
};
</script>