<template>
  <div id="container">
    <div id="mapContainer"></div>
  </div>
</template>

<script>
import "leaflet/dist/leaflet.css";
import L from "leaflet";
import "leaflet.heat"
import { earthquake } from "../assets/earthquake";

export default {
  name: "Map",
  data() {
    return {
      center: [-0.789275,113.921327],
      zoom: 5,
      // data: [
      //   [-6.93,	107.57,	709.00],
      //   [-6.94,	107.58,	697.00],
      //   [-6.94,	107.59,	694.00],
      //   [-6.94,	107.60,	689.00],
      //   [-6.93,	107.60,	695.00],
      //   [-6.95,	107.61,	686.00],
      //   [-6.93,	107.62,	696.00],
      //   [-6.96,	107.64,	670.00],
      //   [-6.96,	107.67,	670.00],
      //   [-6.95,	107.68,	670.00],
      //   [-6.96,	107.69,	666.00],
      //   [-6.93,	107.72,	706.00],
      //   [-6.94,	107.70,	675.00],
      //   [-6.91,	107.70,	698.00],
      //   [-6.92,	107.70,	677.00],
      //   [-6.92,	107.69,	680.00],
      //   [-6.90,	107.67,	690.00],
      //   [-6.90,	107.68,	760.00],
      //   [-6.90,	107.68,	760.00],
      //   [-6.94,	107.64,	682.00],
      //   [-6.91,	107.62,	712.00],
      //   [-6.91,	107.57,	733.00],
      //   [-6.91,	107.60,	700.00],
      //   [-6.90,	107.61,	751.00],
      //   [-6.90,	107.64,	706.00],
      //   [-6.89,	107.63,	750.00],
      //   [-6.88,	107.61,	792.00],
      //   [-6.89,	107.59,	891.00],
      //   [-6.87,	107.58,	856.00],
      //   [-6.87,	107.60,	848.00]
      // ],
      map: null,
    };
  },
  methods: {
    setupLeafletMap () {
      this.map = L.map("mapContainer").setView(this.center, this.zoom);
      L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        attribution: '&copy; <a href="http://osm.org/copyright">OpenStreetMap</a> contributors'
      }).addTo(this.map)

    const points = earthquake
      ? earthquake.map((p) => {
          return [p[0], p[1]];
        })
      : [];

      L.heatLayer(points, {radius: 50}).addTo(this.map);
    },
  },
  mounted() {
    this.setupLeafletMap();
  },
};
</script>

<style scoped>
#container {
  display: flex;
}
#mapContainer {
  width: 100vw;
  height: 100vh;
}
</style>