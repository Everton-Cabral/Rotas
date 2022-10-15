<template>
    <div id="map">
        <l-map style="height: 500px" :zoom="zoom" :center="center">
          <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
          <l-marker v-for="(m, i) in markerLatLng" :key=i :lat-lng="m"></l-marker>
        </l-map>
        <button @click="teste()">Clique</button>
    </div>
</template>

<script>


import { LMap, LTileLayer, LMarker } from 'vue2-leaflet';

export default {
  name: 'MyAwesomeMap',
  components: {
    LMap,
    LTileLayer,
    LMarker,
  },
  data () {
    return {
      url: 'https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png',
      attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
    
      zoom: 14,
      center: [-8.043257675293837, -34.91035939608491],
      markerLatLng: [[-8.053334920083357, -34.89778231644624],[-8.025390333382614, -34.91592141162961]],
     teste: ''
    };
  },
//  methods:{
//   teste(){
//     fetch('https://jsonplaceholder.typicode.com/todos/1')
//   .then(response => response.json())
//   .then(json => console.log(json))
//   }
//  },

 created(){
  const url = 'https://merchant-api.ifood.com.br/authentication/v1.0/oauth/token';
  let data = {
    grantType: 'client_credentials',
    clientId: '33efb8f7-bee2-46ee-8d77-55ae86466e71',
    clientSecret:'pryhaotqjqhvakz1qzsdlbc6xitm1q3f0dperpffevsu5r2x2013lbgihcsgwasrqq1efo1pbru0kuv3ry94z1tzb9ay96wuhf1',
    
  }
  
  let fetchData = {
    method: 'POST',
    body: data,
    headers: new Headers()

  }
  fetch(url, fetchData).then( ()=>{
    console.log('deu bom')
  })
 
 }

}
</script>

<style>
    #map { height: 220px; }
</style>
, {


});