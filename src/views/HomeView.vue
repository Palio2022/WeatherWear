<script>
import { defineComponent } from "vue";
import Kachel from "@/components/kachel.vue";

export default defineComponent({
  components: { Kachel },
  data() {
    return {
      weatherData: {
        morning: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
        },
        noon: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
        },
        evening: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
        },
        night: {
          temperature: null,
          rain: null,
          sunshine: null,
          uv: null,
        }
      }
    };
  },
  mounted() {
    this.fetchData();
  },
  methods: {
    fetchData() {
      const url = "https://api.open-meteo.com/v1/forecast?latitude=52.52&longitude=13.41&hourly=temperature_2m,rain,snowfall,wind_speed_10m&daily=uv_index_max&timezone=Europe%2FBerlin";
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
      const sunshine = data.hourly.sunshine_duration;

      const morningIndex = this.findHourIndex(hours, 6);
      const noonIndex = this.findHourIndex(hours, 12);
      const eveningIndex = this.findHourIndex(hours, 18);
      const nightIndex = this.findHourIndex(hours, 0);
    

      this.weatherData = {
        morning: {
          temperature: temperatures[morningIndex],
          rain: rain[morningIndex],
          sunshine: sunshine ? sunshine[morningIndex] : null,
          uv: uv_index_max[0],
        },
        noon: {
          temperature: temperatures[noonIndex],
          rain: rain[noonIndex],
          sunshine: sunshine ? sunshine[noonIndex] : null,
          uv: uv_index_max[0],
        },
        evening: {
          temperature: temperatures[eveningIndex],
          rain: rain[eveningIndex],
          sunshine: sunshine ? sunshine[eveningIndex] : null,
          uv: uv_index_max[0],
        },
        night: {
          temperature: temperatures[nightIndex],
          rain: rain[nightIndex],
          sunshine: sunshine ? sunshine[nightIndex] : null,
          uv: uv_index_max[0],
        }
      };

      console.log("Processed weather data:", this.weatherData);
    },
    findHourIndex(hours, targetHour) {
      return hours.findIndex(time => new Date(time).getHours() === targetHour);
    }
  }
});
</script>

<template>
  <main class="columns is-fullwidth">
    <kachel class="column" daytime="Vormittags" uv-index="2" weathertyp="rain" :temperature="weatherData.morning.temperature"></kachel>
    <kachel class="column" daytime="Mittags" uv-index="5" weathertyp="sun" :temperature="weatherData.noon.temperature"></kachel>
    <kachel class="column" daytime="Nachmittag" uv-index="5" weathertyp="sun" :temperature="weatherData.evening.temperature"></kachel>
    <kachel class="column" daytime="Abend" uv-index="8" weathertyp="sun" :temperature="weatherData.evening.temperature"></kachel>
    <kachel class="column" daytime="Nacht" uv-index="0" weathertyp="sun" :temperature="weatherData.night.temperature"></kachel>
  </main>
</template>
