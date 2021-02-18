<template>
  <div>
    <div class="map">
      <div id="mapid"></div>
    </div>
    <div class="toolbar">
      <button class="btn btn-primary" @click="markermiCasa">My home</button>
      <button class="btn btn-success" @click="circlemiCasa">My shop</button>
      <button class="btn btn-warning" @click="polJob">My job</button>
      <button class="btn btn-danger" @click="popUpHome">Pop up of my home</button>
    </div>
  </div>
</template>

<script>
import L from "leaflet";
import { onMounted } from "vue";

export default {
  setup() {
    let mymap;
    let marker

    const markermiCasa = () => {
      marker = L.marker([39.70503893448381, 3.4556653312521752]).addTo(mymap);
    };

    const circlemiCasa = () => {
      let circle = L.circle([39.70503893448381, 3.4556653312521752], {
        color: "red",
        fillColor: "#f03",
        fillOpacity: 0.5,
        radius: 500,
      }).addTo(mymap);
    };

    const polJob = () => {
       polygon = L.polygon([
        [39.70503893448381, 3.4556653312521752],
        [39.70753164540888, 3.455708246595724],
        [39.70436209014396, 3.454013090525537],
      ]).addTo(mymap);
    };
    
    const popUpHome =()=>{
      //marker.bindPopup("<b>Hello world!</b><br>I am a popup.").openPopup();
      var popup = L.popup()
    .setLatLng([39.70503893448381, 3.4556653312521752])
    .setContent("I am a standalone popup.")
    .openOn(mymap);
    }


    onMounted(() => {
      mymap = L.map(mapid).setView([39.70503893448381, 3.4556653312521752], 13);

      L.tileLayer(
        "https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}",
        {
          attribution:
            'Map data &copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
          maxZoom: 18,
          id: "mapbox/streets-v11",
          tileSize: 512,
          zoomOffset: -1,
          accessToken:
            "pk.eyJ1IjoiZXN0ZWxvY2siLCJhIjoiY2tsYXFkdHVhM216dDJvcW9waTZ5NmM5MyJ9.flVzZqTwslOjfso10-TfGg",
        }
      ).addTo(mymap);
    });
    return {
      markermiCasa,
      circlemiCasa,
      polJob,
      popUpHome
    };
  },
};
</script>

<style lang="scss" scoped>
.map {
}

#mapid {
  height: 500px;
}
</style>
