<script>
  export default {
    props: {
      uvIndex: Number
    }
  }
</script>

<template>
  <div class="format">
  <!--  Sonnenbrille-->
    <div v-if="this.uvIndex >= 2">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/200655/sunglasses-sun.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey imgBorder" src="https://www.svgrepo.com/show/200655/sunglasses-sun.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>

  <!--HUT-->
    <div v-if="this.uvIndex >= 2">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/169775/cap.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey-light imgBorder" src="https://www.svgrepo.com/show/169775/cap.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>

  <!--  Sonnencreme-->
    <div v-if="this.uvIndex >= 2">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/284653/sun-cream.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey-light imgBorder" src="https://www.svgrepo.com/show/284653/sun-cream.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>

  <!--  T-Shirt  -->
    <div v-if="this.uvIndex >= 2">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/311551/tshirt.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey-light imgBorder" src="https://www.svgrepo.com/show/311551/tshirt.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>

  <!--  Schatten-->
    <div v-if="this.uvIndex >= 5">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/274590/sun-umbrella-yard.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey-light imgBorder" src="https://www.svgrepo.com/show/274590/sun-umbrella-yard.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>

  <!--Im Haus bleiben-->
    <div v-if="this.uvIndex >= 8">
      <img class="has-background-danger imgBorder" src="https://www.svgrepo.com/show/474867/home.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>
    <div v-else>
      <img class="has-background-grey-light imgBorder" src="https://www.svgrepo.com/show/474867/home.svg" alt="IMG NOT FOUND" style="width: 45px;">
    </div>


  </div>
</template>

<style>
.imgBorder {
  border-radius: 10px;
  border-style: solid;
  border-color: black;
  margin: 2px;
}

.format {
  display: flex;
  justify-items: center;
}
</style>