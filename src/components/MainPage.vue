<template>
  <div>
    <TheHeader :weather="weather"></TheHeader>

    <main class="main__content">
      <SearchWeather @cityWeatherFetched="updateWeatherCity"></SearchWeather>
      <UserLocation
        @locationWeatherFetched="updateWeatherLocation"
      ></UserLocation>
    </main>

    <div class="main__data">
      <div class="data" v-if="source === 'city'">
        <!-- Insert your template for displaying weather by city search -->
        <h2 class="data__title">Weather for {{ weather.name }}</h2>
        <p class="data__text">
          Current Temperature: {{ weather.main.temp.toFixed() }}°C
        </p>
        <p class="data__text">
          Weather Today: {{ weather.weather[0].description }}
        </p>
        <p class="data__text">Feels Like : {{ weather.main.feels_like }}°C</p>
        <p class="data__text">
          The Max Temperature: {{ weather.main.temp_max }}°C
        </p>
        <p class="data__text">
          The Lowest Temperature: {{ weather.main.temp_min }}°C
        </p>
        <!-- <img :src="weatherIcon" /> -->
        <!-- More weather details... -->
      </div>

      <!-- Location Weather Template -->
      <div class="data" v-else-if="source === 'location'">
        <!-- Insert your template for displaying weather by location -->
        <h2 class="data__title">Weather for {{ weather.name }}</h2>
        <p class="data__text">
          Current Temperature: {{ weather.main.temp.toFixed() }}°C
        </p>
        <p class="data__text">
          Weather Today: {{ weather.weather[0].description }}
        </p>
        <p class="data__text">Feels Like : {{ weather.main.feels_like }}°C</p>
        <p class="data__text">
          The Max Temperature: {{ weather.main.temp_max }}°C
        </p>
        <p class="data__text">
          The Lowest Temperature: {{ weather.main.temp_min }}°C
        </p>
        <!-- More weather details... -->
      </div>
    </div>

    <!-- City Weather Template -->
  </div>
</template>

<style scoped>
.data__text {
  font-size: 1.2rem;
  color: #000;
  font-weight: 600;
  color: blueviolet;
}
.data__title {
  font-size: 1.5rem;
  color: red;
}
.data {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  gap: 1.5rem;
}
.main__data {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  margin-top: 5rem;
}
.main__content {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin-top: 5rem;
}
</style>

<script>
import UserLocation from "./weathers/userLocation.vue";
import TheHeader from "../Layout/TheHeader.vue";
import SearchWeather from "./weathers/SearchWeather.vue";
export default {
  watch: {
    weather(newVal) {
      console.log(newVal);
    },
  },

  // In MainPage.vue script:
  components: { UserLocation, SearchWeather, TheHeader },
  data() {
    return {
      loading: true,
      weather: null,
      source: null, // this will track whether the weather data is from city search or user's location
    };
  },
  methods: {
    updateWeatherCity(weatherData) {
      this.weather = weatherData;
      this.source = "city";
    },
    updateWeatherLocation(weatherData) {
      this.weather = weatherData;
      this.source = "location";
    },
  },
  computed: {
    weatherIcon() {
      if (!this.weather) return;
      const iconCode = this.weather.weather[0].icon;
      return `http://openweathermap.org/img/wn/${iconCode}.png`;
    },
  },
};
</script>
