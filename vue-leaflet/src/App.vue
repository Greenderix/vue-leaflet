
<!--<template>-->
<!--  <div id="app">-->
<!--    helo-->
<!--    <custom-map></custom-map>-->
<!--  </div>-->
<!--</template>-->


<!--<script>-->
<!--import CustomMap from '@/components/CustomMap.vue'-->
<!--export default {-->
<!--  name: "App",-->
<!--  components:{-->
<!--    CustomMap-->
<!--  },-->
<!--};-->
<!--</script>-->
<!--<style>-->

<!--</style>-->




<template>
  <client-only>
    <div id="mapContainer"></div>
  </client-only>

  <div>
    {{objects}}
  </div>
<!--  <custom-map>-->

<!--  </custom-map>-->


</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import axios from "axios";
import CustomMap from "@/components/CustomMap.vue";


export default {
  name: "LeafletMap",
  components: {CustomMap},
  data() {
    return {
      map: null,
      objects: [],

    };
  },
  mounted() {
    this.resp()
    this.createmap()
    console.log('dsadas');

  },
  onBeforeUnmount() {
    if (this.map) {
      this.map.remove();
    }
  },

  methods: {
    async resp(){
      console.log(this.objects);
      this.showmap=true;
      try{
        await axios.get("/api/objects").then(response => (this.objects = response));
      }
      catch (e) {
        console.log(e)
      }
      finally {

        // this.map.on()
      }

    },
    async createmap(){
      this.map = L.map("mapContainer").setView([46.05, 11.05], 5);
      L.tileLayer("http://{s}.tile.osm.org/{z}/{x}/{y}.png", {
        attribution:
            '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      }).addTo(this.map);
      //use a mix of renderers
      // let customPane = this.map.createPane("customPane");
      // let canvasRenderer = L.canvas({pane: "customPane"});
      // customPane.style.zIndex = 399; // put just behind the standard overlay pane which is at 40
      for (let ob in this.objects){
        console.log(ob.latitude)
        L.marker([ob.latitude, ob.longitude]).addTo(this.map);
        console.log(ob.latitude)
      }

    }

  }

};

</script>

<style scoped>
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>

