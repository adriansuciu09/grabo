<template>
  <div>
    <Navbar @change-page="changePage" />
    <div class="content">
      <h1 v-if="activePage === 'home'">Home</h1>
      <h1 v-if="activePage === 'outdoor'">Outdoor-Planer</h1>
      <h1 v-if="activePage === 'about'">About Us</h1>
    </div>
  </div>

  <Home v-if="activePage === 'home'"/>

  <Button @click="showAddTask = !showAddTask" v-if="activePage === 'outdoor'"/>
  <AddTask v-if="showAddTask && activePage === 'outdoor'" @add-task="addTask" @task-saved="showAddTask=false" />
  <div class="padding" v-if="activePage === 'outdoor'">
  </div>
  <TasksArray @delete-task="deleteTask" @updateWeather="getWeather" :tasks="tasks" v-if="activePage === 'outdoor'"/>

  <About v-if="activePage === 'about'"/>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Button from './components/Button.vue'
import Home from './components/Home.vue'
import TasksArray from './components/TasksArray.vue'
import About from './components/About.vue'
import AddTask from './components/AddTask.vue'
import axios from "axios";

export default {
  name: 'App',
  components: {
    Navbar,
    Button,
    Home,
    TasksArray,
    AddTask,
    About,
  },
  data() {
    return {
      activePage: 'home',
      tasks: [],
      showAddTask: false,
    }
  },
  methods: {
    changePage(page) {
      this.activePage = page;
    },

    deleteTask(id) {
  this.tasks = this.tasks.filter((task) => task.id !== id);
  this.saveTasks();
},
    addTask(task) {
  const taskId = this.tasks.length;
  task.id = taskId;
  this.tasks.push(task);
  this.showAddTask = false;
  this.tasks.sort((a, b) => {
    const comp = new Date(a.date) - new Date(b.date);
    if (comp === 0) {
      const timeA = a.time.toLowerCase();
      const timeB = b.time.toLowerCase();
      if (timeA < timeB) {
        return -1;
      } else if (timeA > timeB) {
        return 1;
      } else {
        return 0;
      }
    } else {
      return comp;
    }
  });
  this.saveTasks();
},
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    getWeather(task) {
      console.log("getWeather" + task.id);
      axios.get(`https://api.open-meteo.com/v1/forecast?latitude=47.81&longitude=9.64&daily=weathercode,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,sunrise,sunset,uv_index_max,uv_index_clear_sky_max,precipitation_sum,rain_sum,showers_sum,snowfall_sum,precipitation_hours,precipitation_probability_max,windspeed_10m_max,windgusts_10m_max,winddirection_10m_dominant,shortwave_radiation_sum,et0_fao_evapotranspiration&forecast_days=1&start_date=${task.date}&end_date=${task.date}&timezone=Europe%2FBerlin`)
          .then((response) => {
            console.log(response.data)
            task.weather = response.data.daily;
          })
          .catch(function (error) {
            task.weather = null;
            if (error.response) {
              // The request was made and the server responded with a status code
              // that falls out of the range of 2xx
              console.log(error.response.data);
              console.log(error.response.status);
              console.log(error.response.headers);
            } else if (error.request) {
              // The request was made but no response was received
              // `error.request` is an instance of XMLHttpRequest in the browser and an instance of
              // http.ClientRequest in node.js
              console.log(error.request);
            } else {
              // Something happened in setting up the request that triggered an Error
              console.log('Error', error.message);
            }
            console.log(error.config);
          })
    },
  },
  created() {
  let savedTasks = JSON.parse(localStorage.getItem('tasks'));
  if (savedTasks && savedTasks.length > 0) {
    this.tasks = savedTasks;
  } else {
    let y = new Date().getUTCFullYear();
    let m = new Date().getUTCMonth() + 1;
    let d = new Date().getUTCDate();
    if (m < 10) {
      m = "0" + m;
    }
    if (d < 10) {
      d = "0" + d;
    }
    let date = y + "-" + m + "-" + d;
    this.tasks = [
      {id: 0, text: 'WETTER', date: date, time: '', description: '', show: true}
    ];
  }
  this.tasks.sort((a, b) => new Date(a.date) - new Date(b.date));
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

.content {
  color: white;
  margin-top: 20px;
  text-align: center;
}
</style>
