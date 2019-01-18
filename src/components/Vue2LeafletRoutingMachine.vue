<template>
  <div style="display: none">
    <slot v-if="ready"></slot>
  </div>
</template>

<script>
import L from 'leaflet'
import { IRouter, IGeocoder, LineOptions } from 'leaflet-routing-machine'

const props = {
  waypoints: {
    type: Array,
    default: () => []
  },
  router: {
    type: IRouter
  },
  plan: {
    type: L.Routing.Plan
  },
  geocoder: {
    type: IGeocoder
  },
  fitSelectedRoutes: {
    type: [String, Boolean],
    default: 'smart'
  },
  lineOptions: {
    type: LineOptions
  },
  routeLine: {
    type: Function
  },
  autoRoute: {
    type: Boolean,
    default: true
  },
  routeWhileDragging: {
    type: Boolean,
    default: false
  },
  routeDragInterval: {
    type: Number,
    default: 500
  },
  waypointMode: {
    type: String,
    default: 'connect'
  },
  useZoomParameter: {
    type: Boolean,
    default: false
  },
  showAlternatives: {
    type: Boolean,
    default: false
  },
  altLineOptions: {
    type: LineOptions
  }
}

export default {
  props,
  name: 'LRoutingMachine',
  data() {
    return {
      ready: false
    }
  },
  mounted() {
    this.add()
    this.ready = true
  },
  beforeDestroy() {
    this.$parent.removeLayer(this)
  },
  methods: {
    add() {
      if (this.$parent._isMounted) {

        const options = {
          waypoints: this.waypoints,
          fitSelectedRoutes: this.fitSelectedRoutes,
          autoRoute: this.autoRoute,
          routeWhileDragging: this.routeWhileDragging,
          routeDragInterval: this.routeDragInterval,
          waypointMode: this.waypointMode,
          useZoomParameter: this.useZoomParameter,
          showAlternatives: this.showAlternatives
        }

        const optionTestNames = ['router, plan, geocoder, lineOptions', 'routeLine', 'altLineOptions']

        optionTestNames.map((optionName) => {
          if (this[optionName] !== undefined) {
            options[optionName] = this[optionName]
          }
        })
        
        L.Routing.control(options).addTo(this.$parent.mapObject)
      }
    }
  }
}
</script>

<style>
@import "../../node_modules/leaflet-routing-machine/dist/leaflet-routing-machine.css";
</style>