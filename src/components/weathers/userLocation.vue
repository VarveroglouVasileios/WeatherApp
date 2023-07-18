<template>
  <div class="location">
    <button @click="getUserLocation" class="location__btn">
      Get my location
    </button>
  </div>
</template>

<style scoped>
.location {
  display: flex;
  align-items: center;
  justify-content: center;
}
.location__btn {
  border: none;
  background: none;
  color: green;
  font-size: 1.5rem;
  cursor: pointer;
}
</style>

<script>
import axios from "axios";
export default {
  data() {
    return {
      weather: null,
    };
  },
  emits: ["locationWeatherFetched"],
  methods: {
    async getUserLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(
          async (position) => {
            const lat = position.coords.latitude;
            const lng = position.coords.longitude;
            try {
              const response = await axios.get(
                `http://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&units=metric&appid=6358248b73905df9f54610ecff53be97`
              );
              this.weather = response.data;
              console.log("coords location api", this.weather.weather);
              this.$emit("locationWeatherFetched", this.weather);
            } catch (error) {
              console.error(error);
            } finally {
              this.loading = false;
            }
          },
          (error) => {
            console.error(error);
          }
        );
      } else {
        alert("Geolocation is not supported by this browser.");
      }
    },
  },
};
</script>
