<template>
<v-card
    class="mx-auto"
    max-width="400"
    color="primary"
  >

    <v-form v-on:submit.prevent="getWeather">
      <v-text-field solo
         placeholder="Enter city name"
        name="location"
         v-model="location">{{ location }}
      </v-text-field>
      <!--<v-btn color="purple" outlined>Search</v-btn>-->
    </v-form>

     <v-list-item two-line>
      <v-list-item-content v-if="weather">
        <v-list-item-title class="headline"> {{ weather.name }}</v-list-item-title>
        <v-list-item-subtitle v-for="(item,index) in weather.weather" :key="index">
            {{ item.main}}
        </v-list-item-subtitle>
      </v-list-item-content>
    </v-list-item>

    <v-card-text >
      <v-row align="center">
        <v-col class="display-3" cols="6">
          {{weather.main.temp}}C
        </v-col>
        <v-col cols="6">
          <v-img
            src="https://cdn.vuetifyjs.com/images/cards/sun.png"
            alt="Sunny image"
            width="92"
          ></v-img>
        </v-col>
      </v-row>
    </v-card-text>



    <div v-if="displayWeather" class="container display-weather-section">
      <div id="coord" class="col-xs-4" v-if="weather">
        <h2>Coordinates:</h2>
                <p><strong>Lng</strong> {{ weather.coord.lon }}</p>
                <p><strong>Lat</strong> {{ weather.coord.lat }}</p>

      </div>
        <!--<coord v-bind:coord="weather.coord"></coord>-->

        <!--<weather-display v-bind:weatherDisplay="weather.weather[0]"></weather-display>
             <temperature v-bind:temperature="weather.main"></temperature>
            <winds v-bind:wind="weather.wind"></winds>
            <clouds v-bind:cloud="weather.clouds"></clouds>
            <sun v-bind:sun="weather.sys"></sun>-->
      </div>
</v-card>

</template>

<script>
import axios from 'axios'

export default {
  name: "Weather",
  props: {},
  data() {
    return {
      location: "",
      apiKey: "906d99a28d07a5319d0a959fdb67e00a",
      weather: {
        coord: {},
        weather:[],
        main: {}
       },
      displayWeather: false,
      coords: {}
    };
  },
  mounted() {
  },
  methods: {
    getWeather() {
      return axios
        .get(
          "http://api.openweathermap.org/data/2.5/weather?q=" +
           this.location +
           '&units=metric' +
            "&appid=" +
            this.apiKey
        )
        .then(
          res => {
            this.weather = res.data;
            console.log(this.weather);


            this.displayWeather = true;
          }
          //  response => {
          //    this.weather = [];
          //    this.displayWeather = false;
          //  }
        );
    }
  }
};
</script>

<style>
</style>