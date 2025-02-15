<script>
import { defineComponent, handleError } from "vue";
import Kachel from "@/components/kachel.vue";

export default defineComponent({
  components: { Kachel },
  data() {
    return {
      cityData: {

      },
      weatherData: {
        morning: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
          wind: null,
          weatherCode: 5

        },
        midday: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
          wind: null,
          weatherCode: 7
        },
        noon: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
          wind: null,
          weatherCode: 50
        },
        evening: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
          wind: null,
          weatherCode: 10
        },
        night: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
          wind: null,
          weatherCode: 1
        }
      },
      currentDate: '',
      currentCity: '',

    };
  },
  mounted() {
    this.fetchData();
    this.setDate();
    this.fetchGeoLocation();
  },
  methods: {
    fetchGeoLocation() {
      if (navigator.geolocation) {
        navigator.geolocation.getCurrentPosition(this.handlePosition, this.handleError);
      } else {
        alert("Geolocation is not supported by this browser.");
      }

    },
    handlePosition(posititon) {
      const { latitude, longitude } = posititon.coords;
      this.fetchData(latitude, longitude);
      this.fetchCityName(latitude, longitude);
      console.log("Fetched Coords: Latitude:", latitude, "Longitude:", longitude);

    },
    handleError(error) {
      console.error('Error fetching location:', error);
      alert('Unable to retrieve your location.');
    },
    fetchCityName(latitude, longitude) {
      const KEY = "pk.fba1a59c9a2ea93e7550959ad88ab7a9"; // https://docs.locationiq.com/docs/reverse-geocoding
      const url = `https://us1.locationiq.com/v1/reverse?key=${KEY}&lat=${latitude}&lon=${longitude}&format=json`;

     
      fetch(url)
        .then(response => response.json())
        .then(data => {
          this.displayCityName(data);
        })
        .catch(error => console.error('Error fetching city name:', error));
    },
    fetchData(latitude, longitude) {
      const url = "https://api.open-meteo.com/v1/forecast?latitude="+ latitude +"&longitude=" + longitude + "&hourly=temperature_2m,rain,weather_code,wind_speed_10m,uv_index&timezone=Europe%2FLondon&forecast_hours=24";
      fetch(url)
        .then(response => response.json())
        .then(data => {
          console.log("Fetched data:", data);
          this.displayData(data);
        })
        .catch(error => console.error('Error fetching weather data:', error));
    },
    displayData(data) {
      const hours = data.hourly.time;
      const temperatures = data.hourly.temperature_2m;
      const rain = data.hourly.rain;
      const sunshine = data.hourly.sunshine_duration || Array(hours.length).fill(0); // Falls keine sunshine_duration vorhanden ist
      const uvValues = data.hourly.uv_index;
      const wind = data.hourly.wind_speed_10m;
      const weatherCode = data.hourly.weather_code;

      const morningIndex = this.findHourIndex(hours, 6);
      const middayIndex = this.findHourIndex(hours, 12);
      const noonIndex = this.findHourIndex(hours, 15);
      const eveningIndex = this.findHourIndex(hours, 18);
      const nightIndex = this.findHourIndex(hours, 0);

      this.weatherData = {
        morning: {
          temperature: temperatures[morningIndex],
          rain: rain[morningIndex],
          sunshine: sunshine[morningIndex],
          uv: uvValues[morningIndex],
          wind: wind[morningIndex],
          weatherCode: weatherCode[morningIndex]
        },
        midday: {
          temperature: temperatures[middayIndex],
          rain: rain[middayIndex],
          sunshine: sunshine[middayIndex],
          uv: uvValues[middayIndex],
          wind: wind[middayIndex],
          weatherCode: weatherCode[middayIndex]
        },
        noon: {
          temperature: temperatures[noonIndex],
          rain: rain[noonIndex],
          sunshine: sunshine[noonIndex],
          uv: uvValues[noonIndex],
          wind: wind[nightIndex],
          weatherCode: weatherCode[noonIndex]
        },
        evening: {
          temperature: temperatures[eveningIndex],
          rain: rain[eveningIndex],
          sunshine: sunshine[eveningIndex],
          uv: uvValues[eveningIndex],
          wind: wind[eveningIndex],
          weatherCode: weatherCode[eveningIndex]
        },
        night: {
          temperature: temperatures[nightIndex],
          rain: rain[nightIndex],
          sunshine: sunshine[nightIndex],
          uv: uvValues[nightIndex],
          wind: wind[nightIndex],
          weatherCode: weatherCode[nightIndex]
        }
      };

      console.log("Processed weather data:", this.weatherData);
    },
    findHourIndex(hours, targetHour) {
      return hours.findIndex(time => new Date(time).getUTCHours() === targetHour);
    },
    setDate() {
      const date = new Date();
      this.currentDate = date.toLocaleDateString('de-DE', { weekday: 'long', year: 'numeric', month: 'long', day: 'numeric' });

    },
    displayCityName(data) {

    this.cityData = data.address.city + ", " + data.address.country;
  }
  },

});
</script>

<template>
  <span class="date"> {{ currentDate }}  </span>
  <div class="date"><img src="https://www.svgrepo.com/show/513450/location-pin.svg" alt="IMG NOT FOUND" style="width: 45px;"><span>{{
    cityData }}</span></div>
  <main class="columns is-fullwidth outerBorder">
    <kachel class="column" daytime="Vormittags" :uv-index="weatherData.morning.uv" :weathertyp="weatherData.morning.weatherCode"
      :temperature="weatherData.morning.temperature" :wind="weatherData.morning.wind" :rain="weatherData.morning.rain">
    </kachel>
    <kachel class="column" daytime="Mittags" :uv-index="weatherData.midday.uv" :weathertyp="weatherData.midday.weatherCode"
      :temperature="weatherData.midday.temperature" :wind="weatherData.midday.wind" :rain="weatherData.midday.rain">
    </kachel>
    <kachel class="column" daytime="Nachmittag" :uv-index="weatherData.noon.uv" :weathertyp="weatherData.noon.weatherCode"
      :temperature="weatherData.noon.temperature" :wind="weatherData.noon.wind" :rain="weatherData.noon.rain"></kachel>
    <kachel class="column" daytime="Abend" :uv-index="weatherData.evening.uv" :weathertyp="weatherData.evening.weatherCode"
      :temperature="weatherData.evening.temperature" :wind="weatherData.evening.wind" :rain="weatherData.evening.rain">
    </kachel>
    <kachel class="column" daytime="Nacht" :uv-index="weatherData.night.uv" :weathertyp="weatherData.night.weatherCode"
      :temperature="weatherData.night.temperature" :wind="weatherData.night.wind" :rain="weatherData.night.rain">
    </kachel>
  </main>
</template>
