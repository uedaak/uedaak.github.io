<template>
  <div>
    <v-row align="baseline" justify="center">
      <v-col class="search-input-col">
        <v-text-field
          v-model="inputCity"
          label="都市名を入力"
          class="search-input"
          @keyup.enter="targetCity = inputCity"
        >
        </v-text-field>
      </v-col>
      <v-col cols="auto">
        <v-btn elevation="5" dark color="green" @click="targetCity = inputCity">
          <v-icon>mdi-magnify</v-icon>
          検索
        </v-btn>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12">
        <WeatherCard :target-city="targetCity" />
      </v-col>
      <v-col v-for="city in cities" :key="city" cols="6" lg="4">
        <WeatherCard :target-city="city" />
      </v-col>
    </v-row>
  </div>
</template>

<script>
import WeatherCard from './WeatherCard';
export default {
  components: {
    WeatherCard,
  },
  data() {
    return {
      inputCity: '',
      targetCity: 'tokyo',
      cities: ['shimamoto', 'seto', 'nara'],
    };
  },
};
</script>

<style>
.search-input-col {
  max-width: 500px;
}
</style>
