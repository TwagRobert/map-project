<script lang="ts">
/* eslint-disable no-undef */
import { defineComponent } from 'vue';
import { computed, ref, onMounted, onUnmounted, watch } from 'vue'
import { useGeolocation } from './useGeolocation'
import { Loader } from '@googlemaps/js-api-loader'

const GOOGLE_MAPS_API_KEY = 'AIzaSyCe3AdGzcbI-BTmDlcdXYztHFu9WONzqnc'


export default defineComponent({
  name: 'App',
  
  setup() {
    const { coords } = useGeolocation()
    const currPos = computed(() => ({
      lat: coords.value.latitude,
      lng: coords.value.longitude
    }))

    const loader = new Loader({ apiKey: GOOGLE_MAPS_API_KEY })
    let  mapDiv = ref(null)
  
    // onMounted(async () => {
    //   await loader.load()
    //   new google.maps.Map(mapDiv.value, {
    //     center: currPos.value,
    //     zoom: 7
    //   }) 

    // })

    return { currPos, mapDiv}

  }
   

});
</script>




<template>
    <div id="map">
        <div class="container">
            <h1>Map project</h1>

            <!-- <div ref="mapDiv" style="width: 100%; height: 80vh" /> -->

            <img src="./assets/img_snow.jpg" alt="Snow">
            <div class="buttons">
                <button class="btn1">Teleport me to somewhere random</button>
                <button class="btn2">Bring me back home</button>
            </div>

            <div class="coordinates">
                <ul>
                    <li>Latitude: {{ currPos.lat.toFixed(2) }}</li>
                    <li>longitude:  {{ currPos.lng.toFixed(2) }}</li>
                </ul>

            </div>


        </div>
    </div>

</template>

