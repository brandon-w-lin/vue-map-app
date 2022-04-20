<script>
import mapboxgl from "mapbox-gl";

export default {
  data: function () {
    return {
      places: [
        { lat: -87.6815, lon: 41.9128, description: "Small Cheval" },
        { lat: -87.6233, lon: 41.8827, description: "The Bean" },
        { lat: -87.6359, lon: 41.8789, description: "The Willis Tower" },
      ],
    };
  },
  mounted: function () {
    mapboxgl.accessToken = process.env.VUE_APP_MAPBOX_API_KEY;
    const map = new mapboxgl.Map({
      container: "map", // container ID
      style: "mapbox://styles/mapbox/streets-v11", // style URL
      center: [-87.6815, 41.9128], // starting position [lng, lat]
      zoom: 9, // starting zoom
    });
    // console.log(map);
    // // Create a default Marker and add it to the map.
    // const marker1 = new mapboxgl.Marker().setLngLat([-87.6815, 41.9128]).addTo(map);
    // console.log(marker1);
    console.log(this.places[0]);
    for (const place of this.places) {
      console.log(place.lat);

      var popup = new mapboxgl.Popup({ offset: 25 }).setText(place.description);
      var el = document.createElement("div");
      el.id = "marker";
      new mapboxgl.Marker(el)
        .setLngLat([place.lat, place.lon])
        .setPopup(popup) // sets a popup on this marker
        .addTo(map);
    }
  },
};
</script>

<template>
  <div class="about">
    <h1>This is an about page</h1>
    <div id="map" class="center"></div>
  </div>
</template>

<style>
body {
  margin: 0;
  padding: 0;
}

#map {
  position: absolute;
  top: 20%;
  bottom: 20%;
  left: 25%;
  /* width: 50%;
  height: 50%; */
}

.center {
  margin: auto;
  width: 50%;
  border: 3px solid green;
  padding: 10px;
}

#marker {
  background-image: url("https://smallcheval.com/wp-content/uploads/SmallCheval-2-2104.jpg");
  background-size: cover;
  width: 50px;
  height: 50px;
  border-radius: 50%;
  cursor: pointer;
}

.mapboxgl-popup {
  max-width: 200px;
}
</style>
