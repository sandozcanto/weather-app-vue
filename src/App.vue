<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          name
          id
          class="search-bar"
          placeholder="Search..."
          v-model="query"
          @keypress="fetchWeather"
        />
      </div>
      <!-- {{info}} -->
      <div class="weather-wrap" v-if="typeof weather.main !='undefined'">
        <div class="location-box">
          <div class="location">{{weather.name}},{{weather.sys.country}}</div>
          <div class="data"></div>
        </div>
        <div class="weather-box">
          <div class="temp">{{Math.round(weather.main.temp)}}</div>
          <div class="weather">{{weather.weather[0].main}}</div>
        </div>
      </div>
    </main>
  </div>
</template>                                     

<script>
// import Vue from "vue";
// import axios from "axios";
// import VueAxios from "vue-axios";

// Vue.use(VueAxios, axios);

export default {
  name: "App",
  components: {},
  data() {
    return {
      api_key: "c8637de3c5672dc81957ff9aab03a2a8",
      url_base: "http://api.openweathermap.org/data/2.5/",
      query: "",
      weather: {},
      info: null,
    };
  },
  methods: {
    fetchWeather(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        )
          .then((res) => {
            return res.json();
          })
          .then(this.setResults);
        // axios
        //   .get(
        //     `${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
        //   )
        //   .then((response) => {
        //     console.log(response.data);
        //   });
      }
    },
    setResults(results) {
      this.weather = results;
      console.log(results);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: "Courier New", Courier, monospace;
}

#app {
  background: cadetblue;
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;

  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

.search-box {
  width: 100%;
  margin-bottom: 30px;
  align-content: center;
}

.search-box .search-bar {
  display: block;
  
  align-content: center;
  padding: 15px;

  color: #313131;

  appearance: none;
  border: none;
  outline: none;

  background: none;

  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px, 16px, 0px, 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-box .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.location-box .data {
  color: #fff;
  font-size: 20px;
  font-weight: 500;
  text-align: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
