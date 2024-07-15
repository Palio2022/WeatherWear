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
        <div> <img :src="kleidungsstueck" alt="IMG NOT FOUND" style="width: 100px;">{{  }}</div>
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
    weathertyp: Number,
    uvIndex: Number,
    wind: Number,
    rain: Number
  },
  computed: {
    kleidungsstueck() {
      if (this.weathertyp >= 51 && this.weathertyp <= 99) {
        return "https://www.svgrepo.com/show/425788/jacket.svg"
      }
      else {
        if(this.temperature < 10){
          return "https://www.svgrepo.com/show/425788/jacket.svg"
        }
        else if (this.temperature >= 10 && this.temperature <= 21 ){
          return "https://www.svgrepo.com/show/260867/hoodie-sweatshirt.svg";
        }
        else if (this.temperature >= 21 ){
          return "https://www.svgrepo.com/show/311551/tshirt.svg";
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
.border {
  margin: 10px;
  padding: 5px;
  border-style: solid;
  border-color: white;
  border-radius: 20px;

}
</style>