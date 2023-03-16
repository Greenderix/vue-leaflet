<!--<template>-->
<!--  <div  style="height:600px; width:800px">-->


<!--      <l-map ref="map" v-model:zoom="zoom" :center="[47.41322, -1.219482]">-->
<!--        <l-tile-layer-->
<!--            url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"-->
<!--            -->
<!--        ></l-tile-layer>-->

<!--      </l-map>-->


<!--  </div>-->
<!--</template>-->

<!--<script>-->
<!--import "leaflet/dist/leaflet.css";-->
<!--import { LMap, LTileLayer, LMarker } from "@vue-leaflet/vue-leaflet";-->

<!--export default {-->
<!--  name: "CustomMap",-->
<!--  components: {-->
<!--    LMap,-->
<!--    LTileLayer,-->
<!--    LMarker,-->
<!--  },-->

<!--  data() {-->
<!--    return {-->
<!--      zoom: 2,-->
<!--    };-->
<!--  },-->
<!--};-->
<!--</script>-->

<!--<style></style>-->







<template>
  <div style="height: 90vh; width: 90vw;">
    <l-map
        ref="map"
        style="height: 90vh; width: 90vw;"
        :zoom="zoom"
        :center="center"
        @update:zoom="zoomUpdated"
        @update:center="centerUpdated"
        @update:bounds="boundsUpdated"
    >
      <l-tile-layer :url="url"></l-tile-layer>
    </l-map>
    <div>zoom: {{zoom}}, center: {{center}}</div>
  </div>
</template>

<script>
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";
// import LDrawToolbar from "vue2-leaflet-draw-toolbar";

export default {
  components: { LMap, LTileLayer},
  data() {
    return {
      url: "http://{s}.tile.osm.org/{z}/{x}/{y}.png",
      zoom: 5,
      center: [35.5, -95.5],
      bounds: null
    };
  },
  methods: {
    zoomUpdated(zoom) {
      this.zoom = zoom;
    },
    centerUpdated(center) {
      this.center = center;
    },
    boundsUpdated(bounds) {
      this.bounds = bounds;
    }
  }
};
</script>