<script>
import {defineComponent} from "vue";
import Kachel from "@/components/kachel.vue";

export default defineComponent({
  components: {Kachel}
})
</script>

<template>
  <main>
    <kachel daytime="Vormittags"></kachel>
    <kachel daytime="Mittag"></kachel>
    <kachel></kachel>
    <kachel></kachel>
  </main>
</template>
