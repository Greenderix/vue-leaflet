<template>
  <div>
    <div id="mapContainer" />
  </div>
</template>

<script>
import { defineComponent, onMounted, onBeforeMount } from 'vue'
import 'leaflet/dist/leaflet.css'
import L from 'leaflet'
export default defineComponent({
  name: 'LMap',
  props: {
    markers: {
      type: Array,
      required: false,
      default: () => []
    }
  },
  setup (props) {
    let map = null
    onMounted(() => {
      console.log(props.markers)
      createMapLayer()
    })
    onBeforeMount(() => {
      if (map) {
        map.remove()
      }
    })
    const createMapLayer = () => {
      map = L.map('mapContainer').setView([-26.8560346, -49.239189], 5)
      L.tileLayer('https://{s}.tile.osm.org/{z}/{x}/{y}.png', {
        attribution:
            '&copy; <a href="https://osm.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(map)
      if (props.markers.length) {
        setMarkers()
      }
    }
    const setMarkers = () => {
      props.markers.map((marker) => {
        return L.marker([marker.latitude, marker.longitude]).addTo(map)
            .bindPopup(marker.name)
      })
    }
  }
})
</script>

<style scoped>
#mapContainer {
  width: 100vw;
  height: calc(100vh - 50px);
}
</style>