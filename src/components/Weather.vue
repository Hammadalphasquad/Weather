<script>
export default {
  data() {
    return {
      query: '',
      weather: null
    }
  },
  methods: {
    fetchWeather(e) {
      if (e.key === "Enter") {
        const api_key = '702716f2227d7a18986b659213962306';
        const url_base = "https://api.openweathermap.org/data/2.5/weather";

        fetch(`${url_base}?q=${this.query}&units=metric&APPID=${api_key}`)
          .then(res => res.json())
          .then((data) => {
            this.weather = data;
          });
      }
    },
    formatDate(timestamp) {
      const date = new Date(timestamp * 1000);
      return date.toDateString();
    }
  }
}
</script>
<template>

  <div>
    <main>
      <div class="search-box">
        <input type="text" class="search-bar" placeholder="Search..." v-model="query" @keypress="fetchWeather" />
      </div>
      <div v-if="weather && weather.main" class="weather-wrap">
        <div class="location-box">
          <div class="location">{{ weather.name }}</div>
          <div class="date">{{ formatDate(weather.dt) }}</div>
          <div class="weather-box">
            <div class="temp">{{ weather.main.temp }}°</div>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>
<style>

#app {
  background-color: burlywood;
  transition: 0.4s;
  display: flex;
  justify-content: center;
}
main {
  min-height: 100vh;
 
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  color: #313131;
  font-size: 20px;
  appearance: none;
  border: none;
  background: none;
  background-color: rgba(255, 255, 255, 0.5);
  border-radius: 0px 16px 0px 16px;
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
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 2255, 0.25);
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

