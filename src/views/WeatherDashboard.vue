<template>
  <v-container>
    <v-row>
      <v-col>
        <Weather></Weather>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import Weather from "../components/Weather";
export default {
  name: "WeatherDashboard",
  components: {
    Weather
  }
};
</script>

<style>
</style>