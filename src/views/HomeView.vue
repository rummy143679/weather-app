<template>
  <div class="container-fluid">
    <div class="row">
      <div class="col-12">
        <div class="input-group">
          <input type="text" class="form-control border-success" placeholder="Search by city...." aria-label="city input" v-model="city" >
          <button class="btn btn-success" type="button" @click="getWeatherData">Search</button>
        </div>
        <div class="row" v-if="weatherData">
          <weather-main :weatherData="weatherData"></weather-main>
          <forecast-cards :city="weatherData.name"></forecast-cards>
        </div>
        <div v-if="error" class="alert alert-danger" role="alert">
          {{ city }} city not found. Please try again.
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import ForecastCards from '../components/ForecastCards.vue';
import WeatherMain from '../components/WeatherMain.vue';

export default {
  name: 'HomeView',
  components: {
    ForecastCards,
    WeatherMain
  },
  data() {
    return {
      weatherData: null,
      city : "",
      error: false,
    }
  },
  methods: {
    getWeatherData() {
      const apikey = process.env.VUE_APP_API_KEY
      this.$axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.city}&appid=${apikey}`).then(response => {
        this.weatherData = response.data;
        this.error = false
      }).catch(error => {
        console.error('There was a problem with the fetch operation:', error)
        this.error = true;
        this.weatherData = null;
        // if(error.response) {
        //   alert("City not found")
        // }
      })
    }
  }
}
</script>
<style scoped>
.container-fluid {
  background-image: url('https://images.unsplash.com/photo-1506748686214-e9df14d4d9d0?crop=entropy&cs=tinysrgb&fit=max&fm=jpg&ixid=MnwzNjUyOXwwfDF8c2VhcmNofDJ8fHdlYXRoZXJ8ZW58MHx8fHwxNjg3NTY5NzA1&ixlib=rb-4.0.3&q=80&w=1080');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
  height: 100vh;
}
</style>
