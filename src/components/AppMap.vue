<template>
    <div id="map">
        <l-map style="height:100vh" :zoom="zoom" :center="center">
          <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
          <l-marker v-for="(m, i) in markerLatLng" :key=i :lat-lng="m" :icon="icon">
            </l-marker>
        </l-map>
       
      
        
    </div>
</template>

<script>


import { LMap, LTileLayer, LMarker, } from 'vue2-leaflet';
import {icon} from 'leaflet'



export default {
  name: 'MyAwesomeMap',
  components: {
    LMap,
    LTileLayer,
    LMarker,

  },
  data () {
    return {
      
      url: 'https://{s}.tile.jawg.io/jawg-dark/{z}/{x}/{y}{r}.png?access-token=7IW55n2s5HpCnVjuigy03eBnPRP8HyQ1BZVMo75WLndC5tdn74Fv2KYScoLT0XdV',
      attribution:
      '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors &copy; <a href="https://carto.com/attributions">CARTO</a>',
    
      zoom: 14.5,
      center: [-8.043257675293837, -34.91035939608491],
      markerLatLng: [[-8.053334920083357, -34.89778231644624],[-8.025390333382614, -34.91592141162961]],
      icon: icon({
        iconUrl: require('../icons/cozinhando.png'),
        iconSize:[36, 42]
      })
    };
    
  },


 created(){
 
 
  //   fetch('http://localhost:3000/')
  // .then(response => response.json())
  // .then(json => console.log(json))
  
 
 }


}
</script>

<style>
    #map { width: 94.5%;}
</style>
, {


});

<!-- https://{s}.basemaps.cartocdn.com/rastertiles/voyager/{z}/{x}/{y}{r}.png -->