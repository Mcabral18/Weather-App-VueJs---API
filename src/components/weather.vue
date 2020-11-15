<template>
  <div class="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          v-model="searchQuery"
          @keypress="fetchApiData"
          class="search-bar"
          placeholder="Search Local..."
        />
      </div>
      <div class="weather-content" v-if="typeof weather.main != 'undefined'">
        <div class="location-content">
          <div class="location">
            {{ weather.name }}, {{ weather.sys.country }}
          </div>
        </div>
      </div>
      <div class="weather-box">
        <div class="temp">45 ºc</div>
        <div class="weather">Rain</div>
      </div>
    </main>
  </div>
</template>

<script>
export default {
  name: "Weather",
  data() {
    return {
      // api_url: "api.openweathermap.org/data/2.5/",
      // api_key: "2cf87f3192adffc810960ecfaad375fd",
      api_key: "0788f03604b1463b13ac0ff86fd29841",
      url_base: "https://api.openweathermap.org/data/2.5/",
      //save the value of the input
      searchQuery: "",
      //save the API information
      weather: {},
    };
  },
  methods: {
    fetchApiData(e) {
      if (e.key == "Enter") {
        fetch(
          `${this.url_base}weather?q=${this.query}&units=metric&APPID={0788f03604b1463b13ac0ff86fd29841}`
        )
          .then((data) => {
            return data.json();
          })
          .then(this.useApiData);
      }
    },
    useApiData(data) {
      this.weather = data;
    },
  },
};
</script>

<style scoped></style>
