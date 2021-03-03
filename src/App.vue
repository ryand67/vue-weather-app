<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input type="text" 
        placeholder="Search..." 
        class="search-bar"
        v-model="query"
        @keyup.enter="fetchWeather">
      </div>

      <div class="weather-wrap" 
      v-if="typeof weather.main !== 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">Monday 20 January 2020</div>
        </div>
        <div class="weather-box">
          <div class="temp">9°F</div>
          <div class="weather">Rain</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>

export default {
  name: 'App',
  data() {
    return {
      api_key: 'a6957c1b49c6ff3ddbf191f7c07846ca',
      url_base: 'api.openweather.org/data/2.5/',
      query: '',
      weather: {}
    }
  },
  methods: {
    fetchWeather() {
      fetch(`api.openweathermap.org/data/2.5/weather?q=${this.query}&appid=${this.api_key}`)
        .then(res => {
          return res.json();
        }).then(this.setResults)
    },
    setResults(results) {
      this.weather = results;
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
  transition: .4s;
}

main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, .25), rgba(0, 0, 0, .75))
}

.search-box {
  width: 100%;
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
  background-color: rgba(255, 255, 255, 0.637);
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

.weather-box {
  text-align: center;
}

.weather-box .temp {
  display: inline-block;
  padding: 10px 25px;
  color: #FFF;
  font-size: 8em;
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

</style>
