<template>

  <div class="border hero ">
    <div class="hero-body has-text-black kachel ">
      <div class="has-text-centered ">
        <div class="title is-4 has-text-black"> {{ this.daytime }}</div>
        <div class="container" style="font-size: large;">
          <div style="display: flex; align-items: center; margin-left: 10px;">
            <img src="https://www.svgrepo.com/show/471978/thermometer-03.svg" alt="IMG NOT FOUND" style="width: 25px;">
            <span style="margin-left: 3px;">{{ this.temperature }}°C</span>
          </div>
          <div style="display: flex; align-items: center; margin-left: 10px;">
             <img src="https://www.svgrepo.com/show/466946/wind-alt.svg" alt="IMG NOT FOUND" style="width: 25px;"> 
             
            <span >{{this.wind}}km/h</span> 
          </div>
         <div style="display: flex; align-items: center; margin-left: 10px;">
           <img src="https://www.svgrepo.com/show/451222/rain.svg" alt="IMG NOT FOUND" style="width:25px;">
           <span style="margin-left: 3px;">
            {{this.rain}}mm
           </span>
           <div>{{ this.weathertyp }}</div>
           
         </div>
         
        </div>
        <!--<div><img src="" alt="Kleidungsstück"></div>-->
        <div>{{ kleidungsstueck }}</div>
      </div>
      <div>
        <div> UV Index: {{ this.uvIndex }}</div>
        <div> Empfohlener UV Schutz: {{ uvMaßnahme }}</div>
      </div>
    </div>
  </div>


</template>

<script>
import { stringifyQuery } from "vue-router";

export default {
  props: {
    daytime: String,
    temperature: Number,
    weathertyp: Number,  
    uvIndex: Number,
    wind: Number,
    rain: Number
  },
  computed: {
    uvMaßnahme() {
      if (this.uvIndex <= 2) {
        return "Kein UV Schutz notwendig"
      }
      else if (this.uvIndex >= 3 && this.uvIndex <= 5) {
        return "Entweder Hut, T-Shirt, Sonnenbrille, Sonnencreme tragen oder im Schatten aufhalten"
      }
      else if (this.uvIndex >= 6 && this.uvIndex <= 7) {
        return "Hut, T-Shirt, Sonnenbrille, Sonnencreme und im Schatten aufhalten"
      }
      else if (this.uvIndex >= 8 && this.uvIndex <= 10) {
        return "Hut, T-Shirt, Sonnenbrille, Sonnencreme, im Schatten aufhalten, zwischen 11 und 16 Uhr im Haus sein"
      }
    },

    kleidungsstueck() {
      if (this.weathertyp >= 51 && this.weathertyp <= 99) {
        return "Jacke"
      }
      else {
        if (this.temperature < 10) {
          return "Jacke, Pullover, Lange Hose"
        }
        else if (this.temperature >= 10 && this.temperature <= 17) {
          return "Pullover, Lange Hose";
        }
        else if (this.temperature >= 16 && this.temperature <= 20) {
          return "T-Shirt, Lange Hose";
        }
        else if (this.temperature >= 21 && this.temperature <= 24) {
          return "Pullover, Kurze Hose";
        }
        else if (this.temperature >= 25) {
          return "T-Shirt, Kurze Hose";
        }
      }
        
      
    }
  },
}
</script>

<style>
.container {
  display: flex;

}


.date {
  font-size: xx-large;
  color: #001d3d;
  font-weight: bold;
}

.outerBorder {
  margin: 15px;
  padding: 10px;
  border-style: solid;
  border-color: #D4A373;
  border-radius: 20px;
}

.kachel {
  background-color: #CCD5AE;
  border-radius: 20px;
}

body {
  background-color: #FAEDCD;
}

.border {
  margin: 10px;
  padding: 5px;
  border-style: solid;
  border-color: white;
  border-radius: 20px;

}
</style>