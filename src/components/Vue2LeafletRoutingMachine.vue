<template>
  <div>
  </div>
</template>

<script>
import L from 'leaflet'
import 'leaflet-routing-machine'

const props = {
  waypoints: {
    type: Array,
    default: () => []
  },
  router: {

  },
  plan: {

  },
  geocoder: {

  },
  fitSelectedRoutes: {

  },
  lineOptions: {

  },
  routeLine: {

  },
  autoRoute: {

  },
  routeWhileDragging: {

  },
  routeDragInterval: {

  },
  waypointMode: {

  },
  useZoomParameter: {

  },
  showAlternatives: {

  },
  altLineOptions: {

  }
}

export default {
  props,
  name: 'LRoutingMachine',
  beforeMount() {
    this.add()
  },
  beforeDestroy() {
    this.remove()
  },
  methods: {
    add() {
      if (this.$parent._isMounted) {
        L.Routing.control({
          waypoints: this.waypoints
        }).addTo(this.$parent.mapObject)
      }
    },
    remove() {
      this.$parent.removeLayer(this)
    }
  }
}
</script>

<style>
@import "../../node_modules/leaflet-routing-machine/dist/leaflet-routing-machine.css";
</style>