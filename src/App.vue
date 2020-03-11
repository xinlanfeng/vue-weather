<template>
  <div id="app">
    <main>
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="请输入要查询的城市"
          v-model="query"
          @keyup.enter="getWeather"
        />
      </div>

      <div class="weather-wrap" v-show="isShowWeather">
        <div class="location-box">
          <div class="location">{{ location }}</div>
          <div class="date">{{ date }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ temp }}℃</div>
          <div class="weather">{{ weather }}</div>
        </div>
      </div>
    </main>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  name: 'App',
  data() {
    return {
      api_key: 'bd1a6d8c0c0d4ebe9744fd4bd61e36b2',
      base_url: 'https://free-api.heweather.net/s6/weather/now',
      query: '',
      location: '',
      temp: '',
      weather: '',
      isShowWeather: false,
    }
  },
  computed: {
    date() {
      const date = new Date()
      date.getFullYear
      date.getMonth + 1
      date.getDate
      return `${date.getFullYear()}年${date.getMonth() +
        1}月${date.getDate()}日`
    },
  },
  methods: {
    getWeather() {
      axios
        .get(`${this.base_url}?location=${this.query}&key=${this.api_key}`)
        .then(res => {
          // console.log(res)
          res = res.data.HeWeather6[0]
          this.location = res.basic.location
          this.temp = res.now.tmp
          this.weather = res.now.cond_txt
          this.isShowWeather = !this.isShowWeather
        })
    },
  },
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
body {
  font-family: '微软雅黑';
}
#app {
  background-image: url('./assets/bg2.jpg');
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
}
main {
  min-height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.1),
    rgba(0, 0, 0, 0.3)
  );
}
.search-box {
  width: 100%;
  margin-bottom: 10px;
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
  background-color: rgba(255, 255, 255, 0.7);
  border-radius: 0px 16px;
  transition: 0.4s;
}
.search-box .search-bar:focus {
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.9);
  border-radius: 16px 0px;
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
  font-size: 30px;
  font-weight: 100;
  text-align: center;
  margin-top: 5px;
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
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  margin: 30px 0;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 48px;
  font-weight: 700;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>
