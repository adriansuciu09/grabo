<template>
<Header />
<Button @click="showAddTask = !showAddTask" />
<AddTask v-if="showAddTask" @add-task="addTask" @task-saved="showAddTask=false"/>
<div class = "padding">
</div>
<TasksArray @delete-task="deleteTask" :tasks="tasks"/>
</template>

<script>
import Button from './components/Button.vue'
import Header from './components/Header.vue'
import TasksArray from './components/TasksArray.vue'
import AddTask from './components/AddTask.vue'

export default {
  name: 'App',
  components: {
    Button,
    Header,
    TasksArray,
    AddTask
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,

    }
  },
  methods: {
    deleteTask(id){
      this.tasks = this.tasks.filter((task) =>task.id !== id)
    },
    addTask(task){
      this.tasks = [...this.tasks, task],
      this.showAddTask = false
    }
  },
  created(){
    this.tasks= [
      {id: 1, text: 'Termin 1', time: 'Montag'},
      {id: 2, text: 'Termin 2', time: 'Dienstag'},
      {id: 3, text: 'Termin 3', time: 'Mittwoch'},
    ]
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
}

.container {
  max-width: 960px;
  margin: 0 auto;
  border: 1px solid teal;
  border-radius: 5px;
}

.btn {
  background-color: teal;
  border: none;
  color: white;
  padding: 15px 32px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 16px;
  margin: 4px 2px;
  cursor: pointer;
  border-radius: 5px;
}

.padding {
  margin-top: 20px;
}
</style>
