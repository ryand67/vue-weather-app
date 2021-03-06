<template>
  <div id="app" :class="typeof weather.main != 'undefined' && weather.main.temp > 50 ? 'warm' : ''">
    <main>
      <div class="search-box">
        <input type="text" 
        placeholder="Search a city..." 
        class="search-bar"
        v-model="query"
        @keyup.enter="fetchWeather">
      </div>

      <div class="weather-wrap" 
      v-if="typeof weather.main !== 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>
        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°F</div>
          <div class="weather-info">
            <p>Min: {{ Math.round(weather.main.temp_min) }}°F</p>
            <p>Max: {{ Math.round(weather.main.temp_max) }}°F</p>
            <p>Feels Like: {{ Math.round(weather.main.feels_like) }}°F</p>
            <p>Wind: {{ Math.round(weather.wind.speed) }}mph</p>
          </div>
          <div class="weather">
            {{ weather.weather[0].main }}
            <img v-bind:src="iconLink" alt="Weather Icon">
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  name: 'App',
  data() {
    return {
      api_key: 'a6957c1b49c6ff3ddbf191f7c07846ca',
      url_base: 'api.openweather.org/data/2.5/',
      query: '',
      weather: {},
      iconLink: ''
    }
  },
  methods: {
    fetchWeather() {
      axios.get(`https://api.openweathermap.org/data/2.5/weather?q=${this.query}&units=imperial&appid=${this.api_key}`)
        .then((res) => {
          res = res.data;
          this.setResults(res);
          this.iconLink = `http://openweathermap.org/img/wn/${res.weather[0].icon}@2x.png`
        })
    },
    setResults(results) {
      this.weather = results;
    },
    dateBuilder() {
      let d = new Date();
      let months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'Octoboer', 'November', 'December'];
      let days = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday'];

      let day = days[d.getDay()];
      let date = d.getDate();
      let month = month = months[d.getMonth()];
      let year = d.getFullYear();

      return `${day} ${date} ${month} ${year}`
    }
  }
}
</script>


<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

body {
  font-family: 'montserrat', sans-serif;
}

#app {
  background-image: url('./assets/cold-bg.jpg');
  background-size: cover;
  background-position: bottom;
  transition: .8s;
}

#app.warm {
  background-image: url('./assets/warm-bg.jpg');
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, 0.74));
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
}

.search-box {
  width: 30%;
  margin-bottom: 2em;
}

.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 1em;
  color: #313131;
  font-size: 1.4em;
  appearance: none;
  outline: none;
  border: none;
  background: none;
  box-shadow: 0px 0px .5em rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, 0.89);
  border-radius: 0px 1em 0em 1em;
  transition: .4s;
}

.search-box .search-bar:focus {
  box-shadow: 0px 0px 1em rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, .75);
  border-radius: 1em 0px 1em 0px;
}

.location-box .location {
  color: #FFF;
  font-size: 2em;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 3px rgba(0, 0, 0, .25);
}

.location-box .date {
  color: #FFF;
  font-size: 1.5em;
  font-weight: 300;
  text-align: center;
  font-style: italic;
}

.weather {
  display: flex;
  justify-content: center;
  align-items: center;
}

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 7em;
  font-weight: 900;

  text-shadow: 3px 6px rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, .25);
  border-radius: 16px;
  margin: 32px 0px;

  box-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.weather-box .weather {
  color: #FFF;
  font-size: 48px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, .25);
}

.weather-info {
  color: #FFF;
  font-size: 2em;
  display: flex;
  flex-direction: row;
}

.weather-info p {
  margin: 0 1em;
}

</style>
