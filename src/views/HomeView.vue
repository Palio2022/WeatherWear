<script>
import {defineComponent} from "vue";
import Kachel from "@/components/kachel.vue";

export default defineComponent({
  components: {Kachel}
})
</script>

<template>
  <main class="columns is-fullwidth">
    <kachel class="column" daytime="Vormittags" uv-index="2" weathertyp="rain" temperature="7"></kachel>
    <kachel class="column" daytime="Mittags" uv-index="5" weathertyp="sun" temperature="16"></kachel>
    <kachel class="column" daytime="Nachmittag" uv-index="5" weathertyp="sun" temperature="25"></kachel>
    <kachel class="column" daytime="Abend" uv-index="8" weathertyp="sun" temperature="21"></kachel>
    <kachel class="column" daytime="Nacht" uv-index="0" weathertyp="sun" temperature="3"></kachel>
  </main>
</template>
