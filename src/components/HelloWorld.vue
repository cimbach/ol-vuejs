<style>
@import "node_modules/ol/ol.css";
.read-the-docs {
  color: #888;
}
.mymap {
  width: 700px;
  height: 500px;
  background-color: white;
}
</style>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="deczoom">Zoom -</button>
    <button type="button" @click="inczoom">Zoom +</button>
    <p>Zoom = {{ count }}</p>
  </div>
  <div id=mymap class=mymap>
  </div>

</template>

<script setup>
import { ref, onMounted } from 'vue'
import Map from 'ol/Map.js';
import OSM from 'ol/source/OSM.js';
import TileLayer from 'ol/layer/Tile.js';
import View from 'ol/View.js';
import {fromLonLat} from 'ol/proj';


const count = ref(11);
var map = null;

defineProps({
  msg: String,
})

const inczoom=()=>{
  count.value=count.value+1;
  const myview=map.getView();
  myview.setZoom(count.value);
}

const deczoom=()=>{
  count.value=count.value-1;
  const myview=map.getView();
  myview.setZoom(count.value);
}

onMounted(()=>{
  console.log("In onMounted");
  map = new Map({
  target: 'mymap',
  layers: [
    new TileLayer({
      source: new OSM(),
    }),
  ],
  view: new View({
    center: fromLonLat([6.6339, 46.5194]), // Coordinates for Lausanne,
    zoom: count.value,
  }),
});
 console.log("map", map)
})


</script>




