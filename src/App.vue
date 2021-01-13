<template>
  <v-app>
    <v-app-bar app dark color="green font-weight-black">
      Weather News
    </v-app-bar>
    <v-main>
      <v-container>
        <WeatherNews />
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import WeatherNews from './components/WeatherNews';
export default {
  name: 'App',
  components: {
    WeatherNews,
  },
};
</script>
