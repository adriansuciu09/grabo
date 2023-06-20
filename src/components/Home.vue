<template>
  <div class="current">
    <p> Aktuelles Wetter in Weingarten:</p>
    <div class="weathercode">
      <i class = "fas fa-sun fa-2xl fa-bounce" v-if="currentWeather?.weathercode<2"/>
      <i class = "fas fa-cloud fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<4"/>
      <i class = "fas fa-smog fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<49"/>
      <i class = "fas fa-cloud-rain fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<56"/>
      <i class = "fas fa-snow fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<58"/>
      <i class = "fas fa-cloud-rain fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<66"/>
      <i class = "fas fa-cloud-rain fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<68"/>
      <i class = "fas fa-snowflake fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<78"/>
      <i class = "fas fa-cloud-showers-heavy fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<83"/>
      <i class = "fas fa-snowflake fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<87"/>
      <i class = "fas fa-cloud-bolt fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<95"/>
      <i class = "fas fa-cloud-bolt fa-2xl fa-bounce" v-else-if="currentWeather?.weathercode<100"/>
    </div>
    <div>
      <i class = "fas fa-temperature-low fa-l"/> Temperatur: {{currentWeather?.temperature}} °C
    </div>
    <div>
      <i class = "fas fa-percent fa-l"></i> Regenrisiko: {{currentWeather?.precipitation_probability}} %
    </div>
  </div>

</template>

<script>
export default {
  name: 'Home-one',
  props: {
    currentWeather: Object,
  }
}
</script>

<style>

html {
  background-color: #3b89f5;
}

.current {
  color: white;
  font-size: 20px;
  margin-bottom: 20px;
}

.current>div{
  padding: 1%;
}
.weathercode>i{
  --fa-animation-duration: 1.5s
}
</style>