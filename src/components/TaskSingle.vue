<template>
  <div class="task">
    <div class="data">
      <h3>{{ task.text }}</h3>
      <p>{{ dateformat(task.date) }}</p>
      <p>{{ task.time }}</p>
      <div>
        <i @click="onShow(task)" class="fas fa-caret-down" v-if="!task.show"></i>
        <i @click="onShow(task)" class="fas fa-caret-up" v-else-if="task.show"></i>
      </div>
      <div>
        <i @click="onDelete(task.id)" id="delete" class="fas fa-times"></i>
      </div>
    </div>
    <div class="description" v-if="task.show && task.description">
      <div><b>Beschreibung:</b></div>
      <div>{{ task.description }}</div>
    </div>
    <div class="weather" v-if="task.show && !task.weather">
      <p>Leider sind für diesen Termin keine Wetterdaten vorhanden!</p>
    </div>
    <div class="weather" v-else-if="task.show && task.weather">
      <p>
        <i class="fas" :class="weatherIconClass(task.weather.weathercode[0])"></i>
      </p>
      <p>
        min./max. Temperatur: <i class="fas fa-temperature-low fa-l"></i><br/>
        {{ task.weather.temperature_2m_min[0] }} °C / {{ task.weather.temperature_2m_max[0] }} °C
      </p>
      <p>
        UV Index: <i class="far fa-sun fa-l"></i><br/>
        {{ task.weather.uv_index_max[0] }}
      </p>
      <p v-if="task.weather.precipitation_sum[0] > 0">
        Niederschlag: <i class="fas fa-droplet fa-l"></i><br/>
        {{ task.weather.precipitation_sum[0] }} mm
      </p>
      <p v-if="task.weather.snowfall_sum[0] > 0">
        Schneefall: <i class="fas fa-snowflake fa-l"></i><br/>
        {{ task.weather.snowfall_sum[0] }} cm
      </p>
      <p>
        Regenrisiko: <i class="fas fa-percent fa-l"></i><br/>
        {{ task.weather.precipitation_probability_max[0] }} %
      </p>
      <p v-if="task.weather.windspeed_10m_max[0] > 0">
        max. Windgeschwindigkeit: <i class="fas fa-wind fa-l"></i><br/>
        {{ task.weather.windspeed_10m_max[0] }} km/h
      </p>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TaskSingle',
  props: {
    task: Object
  },
  methods: {
    onDelete(id) {
      console.log("delete " + id);
      this.$emit('delete-task', id);
    },
    onShow(task) {
      if (!task.show) {
        console.log("show " + task.id);
        this.$emit('updateWeather', task);
      } else {
        console.log("hide " + task.id);
      }
      task.show = !task.show;
    },
    dateformat(date) {
      const array = ["Sonntag", "Montag", "Dienstag", "Mittwoch", "Donnerstag", "Freitag", "Samstag"];
      const day = new Date(date).getDay();
      date = date.match(/\d+/g);
      return array[day] + " " + date[2] + "." + date[1] + "." + date[0];
    },
    weatherIconClass(weatherCode) {
      if (weatherCode < 2) {
        return "fa-sun fa-2xl";
      } else if (weatherCode < 4) {
        return "fa-cloud fa-2xl";
      } else if (weatherCode < 49) {
        return "fa-smog fa-2xl";
      } else if (weatherCode < 56) {
        return "fa-cloud-rain fa-2xl";
      } else if (weatherCode < 58) {
        return "fa-snow fa-2xl";
      } else if (weatherCode < 66) {
        return "fa-cloud-rain fa-2xl";
      } else if (weatherCode < 68) {
        return "fa-cloud-rain fa-2xl";
      } else if (weatherCode < 78) {
        return "fa-snowflake fa-2xl";
      } else if (weatherCode < 83) {
        return "fa-cloud-showers-heavy fa-2xl";
      } else if (weatherCode < 87) {
        return "fa-snowflake fa-2xl";
      } else if (weatherCode < 95) {
        return "fa-cloud-bolt fa-2xl";
      } else {
        return "fa-cloud-bolt fa-2xl";
      }
    }
  }
};
</script>

<style scoped>
.task {
  border-radius: 10px;
  background-color: #f0f0f0;
  margin-left: 10%;
  margin-right: 10%;
}

.task > div {
  margin: 10px;
  display: flex;
}

.data {
  padding: 10px;
  justify-content: space-between;
}

.data > h3 {
  width: 30%;
}

.data > p {
  width: 30%;
}

.data > div {
  text-align: right;
  width: 5%;
}

#delete {
  color: red;
}

.description > div {
  text-align: left;
  margin-left: 1%;
}

.weather {
  justify-content: space-between;
}

.weather > p {
  padding: 1%;
}
</style>
