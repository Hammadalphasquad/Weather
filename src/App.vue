<script setup>
import Weather from './components/Weather.vue'
</script>
<script>
export default {
  name: 'app',
  data() {
    return {
      api_key: '702716f2227d7a18986b659213962306',
      url_base: "https://home.openweathermap.org/api_keys",
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather(e) { // Add the event parameter here
      if (e.key === "Enter") {
        fetch(`${this.url_base}weather?q=${this.query}&units=metric&APPID=${this.api_key}`)
          .then(res => res.json()) // Fix the typo "jason" to "json"
          .then((res) => this.setResults(res)); // Use a function reference here
      }
    },
    setResults(results) {
      this.weather = results;
    }
  }
}
</script>

<template>
  <header><br><br>
<img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />

<br><br>
    <div class="wrapper">
      <Weather/>
    </div>
  </header>


</template>

