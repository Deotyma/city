<template>
  <div style="height:600px; width:800px">
    <l-map ref="map" v-model:zoom="zoom" :center="geolocation">
      <l-tile-layer
        url="https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png"
        layer-type="base"
        name="OpenStreetMap"
      ></l-tile-layer>
    </l-map>
    <select v-model="selectedCity" @change="updateGeolocation">
      <option value="Paris">Paris</option>
      <option value="Lille">Lille</option>
      <option value="Bordeaux">Bordeaux</option>
    </select>
  </div>
</template>

<script setup>
import "leaflet/dist/leaflet.css";
import { ref } from 'vue';
import { LMap, LTileLayer } from "@vue-leaflet/vue-leaflet";

// Définition des coordonnées géographiques des villes
const cities = {
  Paris: { latitude: 48.862877, longitude: 2.3599987 },
  Lille: { latitude: 50.631855, longitude: 3.0469863 },
  Bordeaux: { latitude: 44.85762, longitude: -0.5733793 }
};

// Fonction pour obtenir les coordonnées d'une ville
const getCityGeolocation = (cityName) => {
  return [cities[cityName].latitude, cities[cityName].longitude];
};

const zoom = ref(10); // Ajustez selon le niveau de zoom désiré pour les villes
const selectedCity = ref('Paris');
const geolocation = ref(getCityGeolocation(selectedCity.value));

const updateGeolocation = () => {
  geolocation.value = getCityGeolocation(selectedCity.value);
};
</script>