<template>
  <div style="display: none">
    <slot v-if="ready"></slot>
  </div>
</template>

<script>
import L from 'leaflet'
import { IRouter, IGeocoder, LineOptions } from 'leaflet-routing-machine'
import { findRealParent } from 'vue2-leaflet';

const props = {
  visible: {
    type: Boolean,
    default: true
  },
  waypoints: {
    type: Array,
    required: true
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

// const optionTestNames = [
//   'router',
//   'plan',
//   'geocoder',
//   'lineOptions',
//   'routeLine',
//   'altLineOptions'
// ]

export default {
  props,
  name: 'LRoutingMachine',
  data() {
    return {
      parentContainer: null,
      ready: false,
      layer: null
    }
  },
  mounted() {
    this.parentContainer = findRealParent(this.$parent)
    this.add()
    this.ready = true
  },
  beforeDestroy() {
    return this.layer ? this.layer.remove() : null
  },
  methods: {
    add () {
      if (this.parentContainer._isMounted) {
        const {
          waypoints,
          fitSelectedRoutes,
          autoRoute,
          routeWhileDragging,
          routeDragInterval,
          waypointMode,
          useZoomParameter,
          showAlternatives
        } = this

        const options = {
          waypoints,
          fitSelectedRoutes,
          autoRoute,
          routeWhileDragging,
          routeDragInterval,
          waypointMode,
          useZoomParameter,
          showAlternatives
        }

        const { mapObject } = this.parentContainer
        const routingLayer = L.Routing.control(options)
        routingLayer.addTo(mapObject)
        this.layer = routingLayer
      }
    }
  }
}
</script>

<style>
  @import '../../node_modules/leaflet-routing-machine/dist/leaflet-routing-machine.css';
</style>