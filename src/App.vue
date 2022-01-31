<template>
  <div id="app">
    <button @click="startScan">Start Soft Scan</button>
    <button @click="endScan">End Soft Scan</button>
    <h1>{{ scanned }}</h1>
  </div>
</template>

<script>
import { Plugins } from "@capacitor/core";
const { DataWedge } = Plugins;

export default {
  data() {
    return {
      scanned: 0,
    };
  },
  mounted() {
    this.startListener();
  },
  methods: {
    startListener() {
      DataWedge.addListener("scan", (response) => {
        this.scanned = response.data;
      });
    },
    startScan() {
      DataWedge.startScanning();
    },
    endScan() {
      DataWedge.stopScanning();
    },
  },
};
</script>
