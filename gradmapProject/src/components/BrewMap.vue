<template>
    <div class="row map">
         <h2> {{currentCenter}} , zoom is {{currentZoom}}</h2>
         <l-map 

            @update:zoom="zoomUpdate"
            @update:center="centerUpdate"
            :zoom="zoom" 
            :center="center">
            <l-tile-layer :url="url" :attribution="attribution"></l-tile-layer>
            <l-marker :key="index" v-for="(brew,index) in brews"
                      :lat-lng="latLng(brew.latitude,brew.longitude)">
                      <l-icon
                        :icon-size="brew.iconSize"
                        :icon-url="icon"
                        @click="openPopUp(latLng,'marker')"
                      >
                      </l-icon>
                      <l-popup
                        
                      
                      
                      ><span> {{brew.name}}  {{brew.job}}'de Çalışıyor</span></l-popup>
            </l-marker>

        </l-map>
    </div>
</template>

<script>

import {LMap, LTileLayer, LMarker,LIcon,LPopup} from 'vue2-leaflet';
import L from 'leaflet';
import work from '../assets/work.png'

export default {
    name: "BrewMap",
    props: {
        brews:Array
    },
    
    data: function () {
        return{
            zoom:6,
            center: L.latLng(39.68299235232355, 34.40131974547758),
            currentCenter:L.latLng(39.68299235232355, 34.40131974547758),
            currentZoom:20,
            url:'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
            attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors',
            marker: L.latLng(39.68299235232355, 34.40131974547758),
            icon:work,
            iconSize:[20,20]

        };
    },
    components: {
        LMap,
        LTileLayer,
        LMarker,
        LIcon,
        LPopup
  },
  methods:{
      latLng:function(lat,lng) {
          return L.latLng(lat,lng)
      },
      centerUpdate:function(center){
          this.currentCenter=center
      },
      zoomUpdate:function(zoom){
          this.currentZoom=zoom
      },
      openPopUp (latLng, test) {
      this.test = test;
      this.$refs.features.mapObject.openPopup(latLng);
    }
  }
}

</script>


<style scoped>
    .map {
        height: 100vh;
    }
</style>