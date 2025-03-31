<template>
    <div class="col-12 d-flex justify-content-center mt-2">
        <div class="card" style="width: 30rem;">
            <div class="card-body">
              <h5 class="card-title">{{weatherData.name}}</h5>
              <p class="card-text">Temperature: {{ (weatherData.main.temp - 273.15).toFixed(2) }} °C</p>
              <p class="card-text">Humidity: {{ weatherData.main.humidity }} %</p>
              <p class="card-text">Weather: {{ weatherData.weather[0].description }}</p>
            </div>
        </div>
    </div>
</template>
<script>
    export default {
        props: {
            weatherData: {
                type: Object,
                required: true
            }
        },
        created() {
            if (!this.weatherData) {
                console.error('Weather data is required');
            }else{
                console.log('Weather data:', this.weatherData);
            }
        }
    }
</script>