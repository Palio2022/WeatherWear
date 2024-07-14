<template>
  <div class="border hero">
    <div class="hero-body has-background-info-light has-text-black">
      <div class="has-text-centered">
        <div class="title is-4 has-text-black"> {{this.daytime}}</div>
        <div class="title is-5 has-text-weight-bold has-text-black"> 14 °C</div>
        <div><img src="" alt="Kleidungsstück"></div>
      </div>
      <div>
        <div> UV Index: 6</div>
        <div> Empfohlener UV Schutz: Sonnencreme</div>
      </div>
    </div>
  </div>
</template>

<script>
import {stringifyQuery} from "vue-router";

export default {

  props: {
    daytime: String
  },
  methods:{
  }
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