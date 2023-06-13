<template>
  <div class="background">
    <SelectCity
      v-model:value="state.selected"
      :value="state.selected"
      :cities="nameOfCity"
      @get-weather="getWeather()"
    />
    <!-- <v-card class="mx-auto" max-width="300">
      <v-card-title>Weather in {{ state.city }}</v-card-title>

      <v-card-item>
        <template v-slot:subtitle>
          {{ state.weather }}
          <div id="icon" v-html="state.icon" ></div>
        </template>
      </v-card-item>

      <v-card-text class="py-0">
        <v-row align="center" no-gutters>
          <v-col class="text-h2" cols="6"> {{ state.temp }}° </v-col>
          <v-col class="text-h4">
            {{ state.time }}
          </v-col>
        </v-row>
      </v-card-text>

      <div class="d-flex py-3 justify-space-between">
        <v-list-item density="compact">
          <v-list-item-subtitle>Wind {{ state.wind }} m/s</v-list-item-subtitle>
        </v-list-item>

        <v-list-item density="compact" prepend-icon="mdi-weather-pouring">
          <v-list-item-subtitle
            >Humidity {{ state.humidity }}</v-list-item-subtitle
          >
        </v-list-item>
      </div>
    </v-card> -->
    <WeatherCard
      :city="state.city"
      :weather="state.weather"
      :temp="state.temp"
      :time="state.time"
      :wind="state.wind"
      :humidity="state.humidity"
      :img="state.icon"
    />
  </div>
</template>
<script setup>
import WeatherCard from "./WeatherCard.vue";
import SelectCity from "@/components/SelectCity.vue";
import { reactive, onMounted } from "vue";
import axios from "axios";
let url =
  "http://api.openweathermap.org/data/2.5/weather/?&appid=d0c04e8b31b988d4ffa7157d1c0f14b6";
let nameOfCity = reactive([
  { name: "Moscow", value: 1 },
  { name: "London", value: 2 },
  { name: "Los Angeles", value: 3 },
  { name: "Minsk", value: 4 },
  { name: "San Francisco", value: 5 },
]);
const state = reactive({
  temp: null,
  wind: null,
  city: null,
  weather: null,
  selected: nameOfCity[0].name,
  humidity: null,
  time: null,
  icon:null
});

const getWeather = onMounted(() => {
  axios.get(`${url}&q=${state.selected}`).then((response) => {
    state.temp = Math.round(response.data.main.temp - 273, 15);
    state.wind = response.data.wind.speed;
    state.city = response.data.name;
    state.weather = response.data.weather[0].main;
    state.humidity = response.data.main.humidity;
    let iconImg = response.data.weather[0].icon;
    state.icon = `<img style="width:100px" src="https://openweathermap.org/img/wn/${iconImg}.png">`;
    var s = new Date(response.data.dt).toLocaleTimeString("en-US").split("");
    let digit = s.slice(0, 4).join("");
    state.time = digit;
  });
});
</script>

<style scoped>
.background {
  width: 100%;
  height: 500px;
  margin: auto;
  text-align: center;
}
.backgorund-search {
  display: flex;
  justify-content: center;
  align-items: flex-end;
  gap: 20px;
}
* {
  color: rgb(255, 255, 255);
}
.select {
  width: 300px;
  margin-top: 10px;
  color: rgb(255, 255, 255);
  font-size: 24px;
  background: rgb(104, 89, 241);
  border-radius: 15px;
  text-align: center;
  height: 40px;
}
.select-option {
  background-color: rgb(104, 89, 241);
  border-radius: 10px;
}
.button {
  width: 150px;
  height: 40px;
  border-radius: 15px;
  background: rgb(104, 89, 241);
}
.v-card {
  background-color: rgb(104, 89, 241);
  margin-top: 20px;
  border-radius: 15px;
}
.iconImg {
  widows: 100px;
  height: 100px;
  padding-left: 50px;
}
</style>
