<template>
  <div class="weather">
    <div class="upper">
      <img  src="../../img/cloud-g7394819da_640.png" alt="">
      <img  src="../../img/cloud-g8e88c796b_640.png" alt="">
    </div>
    <h1 v-show="show" v-on:click="show=!show">What's the weather like today?</h1>
    <div class="current_location" v-if="!show">
      <div class="search-box">
        <input
            v-model="query"
            @keypress="fetchWeather"
            type="text"
            class="search-bar"
            placeholder="Search..."
        >
      </div>
      <div class="weather-box">
          <div class="temp">Temperature in {{weather.location.name}} now is {{ weather.current.temp_c }} °C and {{ weather.current.condition.text }}</div>
          <div><img class="current_icon" :src=weather.current.condition.icon alt=""></div>
      </div>
    </div>
    <div class="lower">
      <img  src="../../img/cloudy-g8ded8a3fc_640.png" alt="">
      <img  class="sun" src="../../img/sun-gbb4f656e4_640.png" alt="">
      <img  src="../../img/thunderstorm-g00241095b_640.png" alt="">
    </div>
  </div>
</template>

<script>
export default {
  name: 'TheWeather',
  data() {
    return {
      API_KEY:  'd6db11c803fe4e818bf93157231807',
      url_base: 'http://api.weatherapi.com/v1',
      query:    '',
      weather:  {
        current: {condition:{},},
        location: {},
      },
      show: true,
    }
  },
  methods: {
    fetchWeather(event) {
      if (event.key === 'Enter') {
        this.fetchToAPI()
      }
    },
    fetchToAPI() {
      fetch(`${this.url_base}/current.json?q=${this.query ? this.query : 'Saint Petersburg'}&key=${this.API_KEY}`)
          .then(res => res.json())
          .then(this.setResults)
          .catch(err => console.log(err))
    },
    
    setResults(results) {
      this.weather = results
    },
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Dancing+Script:wght@700&display=swap');
@keyframes pulsing {
  0% { 
    transform: scale(.5)
  }
  50% {
    transform: scale(1)
  }
  100% {
    transform: scale(.5)
  }
}
  .weather {
    margin: 8% auto;
    font-family: 'Dancing Script';
  }
  h1 {
    font-size: 50px;
    cursor: pointer;
    animation: pulsing 3s infinite
  }
  img {
    width: 10%;
    padding: 2rem 2rem;
  }
  .lower img {
    padding: 2rem 3rem;
  }
  .search-box input{
    padding: .5rem .5rem;
    border: none;
  }
  .weather-box {
    margin: 1rem auto;
    max-width: 50%;
    background-color: azure;
    border-radius: 27px;
    padding: 1rem 1rem;
  }
  .weather-box .temp {
  display:          inline-block;
  padding:          10px 25px;
  color:           black;
  font-size:        30px;
  font-weight:      900;
  text-shadow:      3px 6px rgba(0, 0, 0, .25);
  background-color: rgba(255, 255, 255, .25);
  border-radius:    16px;
  margin:           30px 0;
  box-shadow:       3px 6px rgba(0, 0, 0, .25);
}
.current_icon {
  width: 55%;
}



</style>
