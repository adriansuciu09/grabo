<template>
  <div>
    <Navbar @change-page="changePage" />
    <div class="content">
      <h1 v-if="activePage === 'home'">Home</h1>
      <h1 v-if="activePage === 'outdoor'">Outdoor-Planer</h1>
      <h1 v-if="activePage === 'about'">About Us</h1>
    </div>

    <Home v-if="activePage === 'home'" :currentWeather="currentWeather" />

    <Button @click="toggleAddTask" v-if="activePage === 'outdoor'" />
    <AddTask v-if="showAddTask && activePage === 'outdoor'" @add-task="addTask" @task-saved="showAddTask = false" />
    <div class="padding" v-if="activePage === 'outdoor'"></div>
    <TasksArray v-if="activePage === 'outdoor'" :tasks="tasks" @delete-task="deleteTask" @update-weather="updateWeather" />

    <About v-if="activePage === 'about'" />
  </div>
</template>

<script>
import Navbar from './components/Navbar.vue';
import Button from './components/Button.vue';
import Home from './components/Home.vue';
import TasksArray from './components/TasksArray.vue';
import About from './components/About.vue';
import AddTask from './components/AddTask.vue';
import axios from 'axios';

const latitude = 47.81;    //Koordinaten von Weingarten
const longitude = 9.64;

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
      currentWeather: {},
      showAddTask: false,
    };
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
      task.id = this.tasks.length;
      this.tasks.push(task);
      this.showAddTask = false;
      this.sortTasks();
      this.saveTasks();
    },
    saveTasks() {
      localStorage.setItem('tasks', JSON.stringify(this.tasks));
    },
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
    updateWeather(task) {
      const startDate = task.date;
      const endDate = task.date;
      const apiUrl = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&daily=weathercode,temperature_2m_max,temperature_2m_min,apparent_temperature_max,apparent_temperature_min,sunrise,sunset,uv_index_max,uv_index_clear_sky_max,precipitation_sum,rain_sum,showers_sum,snowfall_sum,precipitation_hours,precipitation_probability_max,windspeed_10m_max,windgusts_10m_max,winddirection_10m_dominant,shortwave_radiation_sum,et0_fao_evapotranspiration&forecast_days=1&start_date=${startDate}&end_date=${endDate}&timezone=Europe%2FBerlin`;

      axios
          .get(apiUrl)
          .then((response) => {
            task.weather = response.data.daily;
          })
          .catch((error) => {
            console.log('Error fetching weather data:', error);
            task.weather = null;
          });
    },
    sortTasks() {
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
    },
  },
  created() {
    const savedTasks = JSON.parse(localStorage.getItem('tasks'));
    if (savedTasks && savedTasks.length > 0) {
      this.tasks = savedTasks;
    } else {
      //Dieser Codeabschnitt, ist lediglich zur Demonstration da.
      //Sonst würde hier kein Termin erstellt werden.
      const now = new Date();
      const date = now.toISOString().split('T')[0];      //toISOString: Converts the date to string (format: YYYY-MM-DDTHH:mm:ss.sssZ).
                                                                  // split (T): Splits into array with 2 Elements, "T" is seperator.
                                                                  // with [0], you get the first element in Array: YYYY-MM-DD.
      this.tasks = [
        { id: 0, text: 'Beispieltermin', date: date, time: 'ganztägig', description: 'Hier ist eine Beispielbeschreibung für einen Termin'},
      ];
    }
    this.sortTasks();

    axios
        .get(`https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&hourly=precipitation_probability&current_weather=true&forecast_days=1&timezone=Europe%2FBerlin`)
        .then((response) => {
          this.currentWeather = response.data.current_weather;
          const hour = new Date().getHours();
          this.currentWeather.precipitation_probability = response.data.hourly.precipitation_probability[hour];
        })
        .catch((error) => {
          console.log('Error fetching current weather:', error);
          this.currentWeather = null;
        });
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: black;
  margin-top: 60px;
  min-width: 980px;
}

.container {
  max-width: 980px;
  margin: 0 auto;
  border: 1px solid teal;
  border-radius: 5px;
}

.btn {
  font-weight: bold;
  background-color: #0d519c;
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
  font-weight: bold;
  margin-top: 20px;
  text-align: center;
}
</style>
