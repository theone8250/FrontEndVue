<template>
  <div id="app" :class="weather.main && weather.main.temp > 26 ? 'warm' : ''">
    <div class="container">
      <!-- search bar -->
      <div class="search-box">
        <input
          type="text"
          class="search-bar"
          placeholder="Search....."
          v-model="query"
          @keyup.enter="fetchWeather"
        />
      </div>

      <div class="weather-wrap" v-if="weather.main">
        <div class="location-box">
          <div class="location">{{ weather.name }}</div>
          <div class="date">{{ currentDate }}</div>
        </div>
        <div class="weather-box">
          <div class="temperature">{{ Math.round(weather.main.temp) }}°C</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      <div class="weather-wrap" v-if="weather.message">
        <div class="location-box">
          <div class="location">{{ weather.message }}</div>
          <div class="date">{{ currentDate }}</div>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import dayjs from "dayjs";
import advancedFormat from "dayjs/plugin/advancedFormat";
dayjs.extend(advancedFormat);
export default {
  name: "App",
  data() {
    return {
      api_key: process.env.VUE_APP_WEATHER_KEY,
      base_url: "https://api.openweathermap.org/data/2.5/",
      query: "Hsinchu",
      weather: {},
      date: "",
    };
  },
  methods: {
    async fetchWeather() {
      const data = await fetch(
        `${this.base_url}weather?q=${this.query}&units=metric&APPID=${this.api_key}`
      );
      this.weather = await data.json();
      console.log(
        "%c 🍶 this.weather : ",
        "font-size:20px;background-color: #6EC1C2;color:#fff;",
        this.weather
      );
    },
  },
  created() {
    this.fetchWeather();
  },
  computed: {
    currentDate() {
      // Do: 1st 2nd ... 31st	Day of Month with ordinal
      return dayjs().format(`MMMM Do YYYY`);
    },
  },
};
</script>

<style>
/* 移除預設的padding & margin */
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* 加入背景圖片 */
#app {
  background-image: url("./assets/cold-bg.jpg");
  background-size: cover;
  background-position: 50%;
  transition: 0.5s;
}

/* 加入溫暖圖片的背景 */
#app.warm {
  background-image: url("./assets/warm-bg.jpg");
}

/* container內加入高度與padding讓內容稍微內縮一些 */
.container {
  height: 100vh;
  padding: 25px;
  background-image: linear-gradient(
    to bottom,
    rgba(0, 0, 0, 0.25),
    rgba(0, 0, 0, 0.75)
  );
}

/* 占滿整個寬度*/
.search-box {
  width: 100%;
  margin-bottom: 35px;
}

/* 調整邊角  */
.search-box .search-bar {
  display: block;
  width: 100%;
  padding: 15px;
  transition: all 0.4s ease-in;
  border-radius: 0 16px 0 16px;
  font-size: 20px;
  border: none;
  outline: none;
  background: none;
  background-color: hsla(0, 0%, 100%, 0.5);
}

/* focus時邊框的變化 */
.search-box .search-bar:focus {
  background-color: rgba(255, 255, 255, 0.75);
  box-shadow: 0px 0px 16px rgba(0, 0, 0, 0.25);
  border-radius: 16px 0px 16px 0px;
  border: 3px solid;
  animation-name: Glow;
  animation-duration: 6s;
  animation-iteration-count: infinite;
}

/* focus時邊框的變色 */
@-webkit-keyframes Glow {
  0% {
    border-color: #ea2027;
  }

  10% {
    border-color: #ee5a24;
  }

  20% {
    border-color: #ffc312;
  }

  30% {
    border-color: #c4e538;
  }

  40% {
    border-color: #009432;
  }

  50% {
    border-color: #0652dd;
  }

  60% {
    border-color: #12cbc4;
  }

  70% {
    border-color: #fda7df;
  }

  80% {
    border-color: #9980fa;
  }

  90% {
    border-color: #b53471;
  }

  100% {
    border-color: #6f1e51;
  }
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
  margin-top: 15px;
}

.weather-box .temperature {
  display: inline-block;
  padding: 10px 25px;
  color: #fff;
  font-size: 102px;
  font-weight: 900;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.25);
  border-radius: 16px;
  box-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}

.weather-box .weather {
  font-size: 48px;
  color: #fff;
  font-weight: 700;
  font-style: italic;
  text-shadow: 3px 6px rgba(0, 0, 0, 0.25);
}
</style>