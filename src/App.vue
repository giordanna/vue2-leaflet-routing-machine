<template>
  <div id="app">
    <l-map :zoom="zoom" :center="center">
      <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
      <l-routing-machine :waypoints="waypoints"></l-routing-machine>
    </l-map>
  </div>
</template>

<script>
import { LMap, LTileLayer } from 'vue2-leaflet'
import LRoutingMachine from './components/Vue2LeafletRoutingMachine.vue'
import L from 'leaflet'

export default {
  components: { LMap, LTileLayer, LRoutingMachine },
  data () {
    return {
      zoom: 6,
      center: L.latLng(38.7436056, -2.2304153),
      url:'http://{s}.tile.osm.org/{z}/{x}/{y}.png',
      attribution:'&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors',
      waypoints: [
        L.latLng(38.7436056, -9.2304153),
        L.latLng(38.7436056, -0.1312811)
      ]
    }
  }
}

</script>

<style>
@import "../node_modules/leaflet/dist/leaflet.css";

html, body, #app {
  height: 100%;
  margin: 0;
}
</style>