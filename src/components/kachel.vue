<template>
  <div class="border hero">
    <div class="hero-body has-background-info-light has-text-black">
      <div class="has-text-centered">
        <div class="title is-4 has-text-black"> {{this.daytime}}</div>
        <div class="title is-5 has-text-weight-bold has-text-black"> 14 °C</div>
<!--        <div><img src="" alt="Kleidungsstück"></div>-->
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
import {stringifyQuery} from "vue-router";

export default {
  props: {
    daytime: String,
    temperature: Number,
    weathertyp: String,  //rain, sun, snow
    uvIndex: Number,

  },
  computed: {
    uvMaßnahme() {
      if(this.uvIndex <= 2){
        return "Kein UV Schutz notwendig"
      }
      else if(this.uvIndex >= 3 && this.uvIndex <= 5){
        return "Entweder Hut, T-Shirt, Sonnenbrille, Sonnencreme tragen oder im Schatten aufhalten"
      }
      else if(this.uvIndex >= 6 && this.uvIndex <= 7){
        return "Hut, T-Shirt, Sonnenbrille, Sonnencreme und im Schatten aufhalten"
      }
      else if(this.uvIndex >= 8 && this.uvIndex <= 10){
        return "Hut, T-Shirt, Sonnenbrille, Sonnencreme, im Schatten aufhalten, zwischen 11 und 16 Uhr im Haus sein"
      }
    },

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
.border{
  padding: 10px;
  border-style: solid;
  border-color: white;
  border-radius: 5px;

}
</style>