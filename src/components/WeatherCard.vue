<template>
  <v-card>
    <v-card-text class="text-center">
      <img alt="icon" :src="weatherIcon" />
      <v-row>
        <v-col cols="12" sm="6" md="4">都市: {{ cityName }}</v-col>
        <v-col cols="12" sm="6" md="4">気温: {{ temp }}℃</v-col>
        <v-col cols="12" sm="6" md="4">天気: {{ weather }}</v-col>
        <v-col cols="12" sm="6" md="4">気圧: {{ pressure }} hPa</v-col>
        <v-col cols="12" sm="6" md="4">最高気温: {{ highestTemp }}℃</v-col>
        <v-col cols="12" sm="6" md="4">最低気温: {{ lowestTemp }}℃</v-col>
      </v-row>
    </v-card-text>
  </v-card>
</template>

<script>
import axios from 'axios';
export default {
  props: {
    targetCity: {
      type: String,
      default: 'tokyo',
    },
  },
  data() {
    return {
      weatherIcon: '',
      cityName: '',
      weather: '',
      temp: '',
      highestTemp: '',
      lowestTemp: '',
      pressure: '',
    };
  },
  watch: {
    targetCity() {
      this.getWeather();
    },
  },
  created() {
    this.getWeather();
  },
  methods: {
    getWeather() {
      axios
        .get('https://api.openweathermap.org/data/2.5/weather', {
          params: {
            q: this.targetCity,
            appid: process.env.VUE_APP_OW_APIKEY,
            units: 'metric',
            lang: 'ja',
          },
        })
        .then(response => {
          const data = response.data;
          this.weatherIcon =
            'https://openweathermap.org/img/wn/' +
            data.weather[0].icon +
            '@2x.png';
          this.weather = data.weather[0].description;
          this.cityName = data.name;
          this.temp = data.main.temp;
          this.highestTemp = data.main.temp_max;
          this.lowestTemp = data.main.temp_min;
          this.pressure = data.main.pressure;
        })
        .catch(error => {
          console.log(error);
          this.$toasted.error('都市が見つかりませんでした');
        });
    },
  },
};
</script>
