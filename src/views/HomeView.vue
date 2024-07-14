<script>
import {defineComponent} from "vue";
import Kachel from "@/components/kachel.vue";

export default defineComponent({
  components: {Kachel}
})
</script>

<template>
  <main>
    <kachel daytime="Vormittags" uv-index="7" weathertyp="rain" temperature="-11"></kachel>
  </main>
</template>
