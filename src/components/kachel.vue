<template>
  
     <div class="border hero ">
    <div class="hero-body has-text-black kachel ">
      <div class="has-text-centered ">
        <div class="title is-4 has-text-black"> {{this.daytime}}</div>
        <div class="title is-5 has-text-weight-bold has-text-black "> <img src="https://www.svgrepo.com/show/471978/thermometer-03.svg" alt="IMG NOT FOUND" style="width: 45px;">{{ this.temperature }} °C</div>
        <div class="title is-5 has-text-weight-bold has-text-black"> <img src="https://www.svgrepo.com/show/466946/wind-alt.svg" alt="IMG NOT FOUND" style="width: 45px;"> {{ this.wind }} km/h</div>
        <div class="title is-5 has-text-weight-bold has-text-black"> <img src="https://www.svgrepo.com/show/451222/rain.svg" alt="IMG NOT FOUND" style="width: 45px;">{{ this.rain }} mm</div>
      
<!--        <div><img src="" alt="Kleidungsstück"></div>-->
        <div>{{ kleidungsstueck }}</div>
      </div>
      <div>
        <div> UV Index: {{ this.uvIndex }}</div>
        <div> Empfohlener UV Schutz: </div>
        <div>
          <UVPicFormatter :uvIndex="this.uvIndex"></UVPicFormatter>
        </div>
      </div>
    </div>
  </div>
  
 
</template>

<script>
import {stringifyQuery} from "vue-router";
import UVPicFormatter from "@/components/UVPicFormatter.vue";

export default {
  components: { UVPicFormatter },
  props: {
    daytime: String,
    temperature: Number,
    weathertyp: String,  //rain, sun, snow
    uvIndex: Number,
    wind: Number,
    rain: Number
  },
  computed: {
    kleidungsstueck() {
      if (this.weathertyp.includes("rain") || this.weathertyp.includes("snow")){
        return "Jacke"
      }
      else if (this.weathertyp.includes("sun")){
        if(this.temperature < 10){
          return "Jacke, Pullover, Lange Hose"
        }
        else if (this.temperature >= 10 && this.temperature <= 17 ){
          return "Pullover, Lange Hose";
        }
        else if (this.temperature >= 16 && this.temperature <= 20 ){
          return "T-Shirt, Lange Hose";
        }
        else if (this.temperature >= 21 && this.temperature <= 24 ){
          return "Pullover, Kurze Hose";
        }
        else if (this.temperature >= 25 ){
          return "T-Shirt, Kurze Hose";
        }
      }
    }
  },
}
</script>

<style>
.date {
  font-size: xx-large;
  color: #001d3d;
  font-weight: bold;
}
.outerBorder{
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
.border{
  margin: 10px;
  padding: 10px;
  border-style: solid;
  border-color: white;
  border-radius: 20px;

}
</style>