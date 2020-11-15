<template>
  <div class="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          v-model="searchQuery"
          @keypress.enter="sendApiRequest"
          class="search-bar"
          placeholder="Search Local..."
        />
      </div>
      <div class="weather-content" v-if="typeof weather.main != 'undefined'">
        <div class="location-content">
          <div class="location">
            {{ weather.name }}
          </div>
        </div>
      </div>
      <div class="weather-box">
        <div class="temp">{{ weather.main.temp }} ºc</div>
        <div class="weather">Wind : {{ weather.wind.speed }}</div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Weather",
  //store variables wuth data
  data() {
    return {
      api_key: "f6a2c317f97367bfe8fa3e5fc517e80d",
      url_base: "https://api.openweathermap.org/data/2.5/",
      //save the value of the input
      searchQuery: "",
      //save the API information
      weather: {},
    };
  },
  methods: {
    sendApiRequest() {
      fetch(
        `${this.url_base}weather?q=${this.searchQuery}&APPID=2cf87f3192adffc810960ecfaad375fd`
      )
        .then((data) => {
          //see the api date before being converted to json
          console.log(data);
          return data.json();
        })
        .then(this.useApiData);
    },
    useApiData(data) {
      this.weather = data;
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
  font-family: "montserrat", sans-serif;
}

.app {
  background-image: url(./assets/main.png);
  background-position: center center;
  background-size: cover;
  transition: 0.4s;
  -webkit-transition: 0.4s;
  -moz-transition: 0.4s;
  -ms-transition: 0.4s;
  -o-transition: 0.4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(117, 115, 115, 0.25),
    rgba(134, 131, 131, 0.75)
  );
}

.search-box {
  width: 50%;
  margin: 10% auto;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;

  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 8px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
  transition: 0.4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 16px 0px 16px 0px;
}

.location-content .location {
  color: #fff;
  font-size: 32px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, 0.25);
}

.weather-box {
  text-align: center;
}

.temp {
  text-align: center;
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px auto;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
