<template>
    <div class="container" :class="typeof weather.main != 'undefined' && weather.main.temp > 16 ? 'warm' : ''">
      <main>
        <div class="search-box">
          <input type="text" class="search" placeholder="Search..." v-model="query"
          @keypress="fetchWeather" />
        </div>

        <div class="weather-wrap" v-if="typeof weather.main != 'undefined'">
        <div class="location-box">
          <div class="location">{{ weather.name }}, {{ weather.sys.country }}</div>
          <div class="date">{{ dateBuilder() }}</div>
        </div>

        <div class="weather-box">
          <div class="temp">{{ Math.round(weather.main.temp) }}°c</div>
          <div class="weather">{{ weather.weather[0].main }}</div>
        </div>
      </div>
      </main>
    </div>
</template>

<script>
    export default {
      name: "HomeComp",
      data() {
        return {
          apiKey: "2e355e0c6cada95b1fb0565448522ce5",
          url: 'https://api.openweathermap.org/data/2.5/',
          query: '',
          weather: {}
        }
      },
      methods: {
        fetchWeather (e) {
          if (e.key == "Enter") {
            fetch(`${this.url}weather?q=${this.query}&units=metric&APPID=${this.apiKey}`)
              .then(data => {
                return data.json();
              }).then((data)=>{
                 this.weather = data;
                console.log(this.weather)
              })
          }
        },
        dateBuilder () {
          let d = new Date();
          let months = ["January", "February", "March", "April", "May", "June", "July", "August", "September", "October", "November", "December"];
          let days = ["Sunday", "Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday"];
          let day = days[d.getDay()];
          let date = d.getDate();
          let month = months[d.getMonth()];
          let year = d.getFullYear();
          return `${day}, ${date} ${month} ${year}`;
        }
      }
    };
    </script>

<style scoped>
    .container {
  width: 320px;
  height: 90vh;
  background: #000;
  background-image: url("../assets/cold-bg.jpg");
  background-size: cover;
  background-position: bottom;
  transition: 0.4s;
  margin: 5vh auto;
}
.container.warm {
  background-image: url('../assets/warm-bg.jpg');
}
main {
  min-height: 100%;
  padding: 25px;
  background-image: linear-gradient(to bottom, rgba(0, 0, 0, 0.35), rgba(0, 0, 0, 0.50));
}
.search-box {
  width: 100%;
  margin-bottom: 30px;
}
.search-box .search {
  display: block;
  width: 100%;
  padding : 10px;
  color: #313131;
  font-size: 15px;
  appearance: none;
  border:none;
  outline: none;
  background: none;
  box-shadow: 0px 0px 10px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.8);
  border-radius: 0px 15px 0px 15px;
  transition: 0.4s;
}
.search-box .search:focus {
  box-shadow: 0px 0px 15px rgba(0, 0, 0, 0.25);
  background-color: rgba(255, 255, 255, 0.75);
  border-radius: 15px 0px 15px 0px;
}
.location-box .location {
  color: #fff;
  font-size: 30px;
  font-weight: 500;
  text-align: center;
  text-shadow: 1px 2px rgba(0, 0, 0, 0.25);
}
.location-box .date {
  color: #fff;
  font-size: 20px;
  font-weight: 300;
  font-style: italic;
  text-align: center;
}
.weather-box {
  text-align: center;
}
.weather-box .temp {
  display: inline-block;
  padding: 10px 20px;
  color: #fff;
  font-size: 100px;
  font-weight: 900;
  text-shadow: 2px 5px rgba(0, 0, 0, 0.25);
  background-color:rgba(255, 255, 255, 0.25);
  border-radius: 15px;
  margin: 30px 0px;
  box-shadow: 5px 5px rgba(0, 0, 0, 0.25);
}
.weather-box .weather {
  color: #fff;
  font-size: 50px;
  font-weight: 700;
  font-style: italic;
  text-shadow: 5px 5px rgba(0, 0, 0, 0.25);
}
</style>