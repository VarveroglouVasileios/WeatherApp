<template>
  <header>
    <img :src="weatherGif" alt="Weather Gif" class="weather__gif" />
  </header>
</template>

<script>
import sunny from "../assets/sunny.gif";
import rainy from "../assets/rainny.gif";
import snowy from "../assets/snow.gif";
import cloudy from "../assets/cloud.gif";
export default {
  props: {
    weather: {
      type: Object,
      default: null,
    },
  },
  computed: {
    weatherGif() {
      if (!this.weather) return;
      const mainWeather = this.weather.weather[0].main.toLowerCase();
      console.log(mainWeather);
      switch (mainWeather) {
        case "clouds":
          return cloudy;
        case "clear":
          return sunny;
        case "rain":
          return rainy;
        case "snow":
          return snowy;
        // Add more cases as needed...
        default:
          return sunny;
      }
    },
  },
};
</script>

<style scoped>
header {
  display: flex;
  flex-direction: row;
  height: 55vh; /* Define the height you want here */
  overflow: hidden;
  background-color: lightgray;
}

.weather__gif {
  width: 100%;
  height: 100%;
  object-fit: fill;
  object-position: center;
}
</style>
