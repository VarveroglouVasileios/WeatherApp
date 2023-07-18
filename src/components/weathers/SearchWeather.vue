<template>
  <div>
    <form @submit.prevent="getWeather">
      <div class="form__control">
        <input
          type="search"
          name="search"
          placeholder="Enter a city"
          v-model.trim="enteredWeather"
        />
        <button class="submit__btn">Search</button>
      </div>
    </form>
  </div>
</template>

<style scoped>
.form__control {
  display: flex;
  flex-direction: row;
  align-items: center;
  justify-content: center;
}
input[type="search"] {
  position: relative;
  background: none;
  border: 0.2rem solid green;
  padding: 0.6rem 0.6rem;
  border-top-left-radius: 10px;
  border-bottom-left-radius: 10px;
  border-top-right-radius: 10px;
  border-bottom-right-radius: 10px;
}
input[type="search"]::placeholder {
  color: black;
  font-size: 1.4rem;
  font-weight: 400;
  font-family: "Gill Sans", "Gill Sans MT", Calibri, "Trebuchet MS", sans-serif;
}

.submit__btn {
  position: absolute;
  border: none;
  background: none;
  color: green;
  font-size: 1.3rem;
  margin-left: 10rem;
  cursor: pointer;
  border-left: 0.2rem solid red;
  border-width: 100%;
  padding: 0.3rem;
  line-height: 0;
  display: flex;
  align-items: center;
  height: 2.8rem; /* Adjust this to the desired height of your button */
}
</style>

<script>
import axios from "axios";
export default {
  emits: ["cityWeatherFetched"],
  data() {
    return {
      enteredWeather: "",
    };
  },
  methods: {
    async getWeather() {
      try {
        const res = await axios.get(
          `http://api.openweathermap.org/data/2.5/weather?q=${this.enteredWeather}&units=metric&appid=6358248b73905df9f54610ecff53be97`
        );
        console.log(res);
        // In getWeather method of SearchWeather.vue:
        this.$emit("cityWeatherFetched", res.data);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>
