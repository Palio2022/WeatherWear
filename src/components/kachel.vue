<template>
  <div class="border hero">
    <div class="hero-body has-background-info-light has-text-black">
      <div class="has-text-centered">
        <div class="title is-4 has-text-black"> {{ daytime }}</div>
        <div id="temperature" class="title is-5 has-text-weight-bold has-text-black"> 14 °C</div>
        <div><img src="" alt="Kleidungsstück"></div>
      </div>
      <div>
        <div> UV Index: 6</div>
        <div> Empfohlener UV Schutz: Sonnencreme</div>
      </div>
      <div id="weather-details">
        <div id="morning-temperature"></div>
        <div id="noon-rain"></div>
        <div id="evening-temperature"></div>
        <div id="night-temperature"></div>
       
      </div>
    </div>
  </div>
</template>

<script>
const url = "https://api.open-meteo.com/v1/forecast?latitude=48.1372&longitude=11.5755&hourly=temperature_2m,rain,sunshine_duration&timezone=Europe%2FBerlin&forecast_days=1&models=icon_seamless";

export default {
  props: {
    daytime: String
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      fetch(url)
        .then(response => response.json())
        .then(data => this.displayData(data))
        .catch(error => console.error('Error fetching weather data:', error));
    },
    displayData(data) {
      const hours = data.hourly.time;
      const temperatures = data.hourly.temperature_2m;
      const rain = data.hourly.rain;
      const sunshine = data.hourly.sunshine_duration;

      const morningIndex = this.findHourIndex(hours, 6);
      const noonIndex = this.findHourIndex(hours, 12);
      const eveningIndex = this.findHourIndex(hours, 18);
      const nightIndex = this.findHourIndex(hours, 0);

      const weatherData = {
        morning: {
          temperature: temperatures[morningIndex],
          rain: rain[morningIndex],
          sunshine: sunshine[morningIndex]
        },
        noon: {
          temperature: temperatures[noonIndex],
          rain: rain[noonIndex],
          sunshine: sunshine[noonIndex]
        },
        evening: {
          temperature: temperatures[eveningIndex],
          rain: rain[eveningIndex],
          sunshine: sunshine[eveningIndex]
        },
        night: {
          temperature: temperatures[nightIndex],
          rain: rain[nightIndex],
          sunshine: sunshine[nightIndex]
        }
      };

      document.getElementById("morning-temperature").innerText = "Morning Temperature: " + weatherData.morning.temperature + "°C";
      document.getElementById("noon-temperature").innerText = "Noon Temperature: " + weatherData.noon.temperature + "°C";
      document.getElementById("evening-temperature").innerText = "Evening Temperature: " + weatherData.evening.temperature + "°C";
      document.getElementById("night-temperature").innerText = "Night Temperature: " + weatherData.night.temperature + "°C";
      document.getElementById("morning-rain").innerText = "Morning Rain: " + weatherData.morning.rain + "mm";
      document.getElementById("noon-rain").innerText = "Noon Rain: " + weatherData.noon.rain + "mm";
      document.getElementById("evening-rain").innerText = "Evening Rain: " + weatherData.evening.rain + "mm";
      document.getElementById("night-rain").innerText = "Night Rain: " + weatherData.night.rain + "mm";
      document.getElementById("morning-sunshine").innerText = "Morning Sunshine: " + weatherData.morning.sunshine + "min";
      document.getElementById("noon-sunshine").innerText = "Noon Sunshine: " + weatherData.noon.sunshine + "min";
      document.getElementById("evening-sunshine").innerText = "Evening Sunshine: " + weatherData.evening.sunshine + "min";
      document.getElementById("night-sunshine").innerText = "Night Sunshine: " + weatherData.night.sunshine + "min";
    },
    findHourIndex(hours, targetHour) {
      return hours.findIndex(time => new Date(time).getHours() === targetHour);
    }
  }
}
</script>

<style>
.border {
  padding: 10px;
  border-style: solid;
  border-color: white;
  border-radius: 5px;
}
</style>
