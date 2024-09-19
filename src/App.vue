<script setup>
import { ref } from "vue";
import Itinerary from './components/Itinerary.vue';
import ItineraryItem from './components/ItineraryItem.vue';
import itineraryData from './data/itinerary.json';

//mapbox imports
import Map from './components/Map.vue';
import '/node_modules/mapbox-gl/dist/mapbox-gl.css';

const data = itineraryData
const showFiles = ref(false)
const showCost = ref(false)
const showCountries = ref(false)
const mapView = ref(false)
const countryFilterBtn = ref('Filter Countries')
const filteredCountriesList = ref([])
const loggedIn = ref(true)
const password = '9mattandem&@!'
const enteredPassword = ref('')
const countries = ref(['South Africa', 'Germany', 'France', 'Netherlands', 'Czechia', 'Slovenia', 'Italy'])
const viewBtnText = ref('Map View')

function logIn (){
  if(enteredPassword.value === password){
    loggedIn.value = true
  }
}

//toggle filter countries button
function filterCountries(){
  showCountries.value = !showCountries.value
  if(showCountries.value === true) {
    countryFilterBtn.value = 'Clear Filter'
  } else {
    countryFilterBtn.value = 'Filter Countries'
  }
  
}

//filter which countries are displayed
function filterCountriesList(countries){
  var filter = false
  filteredCountriesList.value.forEach(element => {
    if(countries.includes(element)){
      filter = true
    }
  });
  if(showCountries.value === false || (showCountries.value === true && filter)){
    return true
  }
  return false
}

//toggles map and text view
function toggleView(){
  mapView.value = !mapView.value
  if(mapView.value === true){
    viewBtnText.value = 'Text View'
  } else {
    viewBtnText.value = 'Map View'
  }

}
</script>

<template>


  <!-- Login Div -->
  <div>
    <div class="h-40 w-80 bg-slate-200 rounded-lg p-5 absolute top-0 bottom-0 left-0 right-0 m-auto">
      <div class="text-center">
        <p class="mb-5 font-semibold">Enter Password to Continue</p>
        <p class="mb-5"><input type="password" name="password" v-model="enteredPassword" class="rounded-lg bg-white"></p>
        <button @click="logIn" class="rounded-lg bg-gray-100 p-2 font-semibold">Continue</button>
      </div>
      
    </div>
  </div>

</template>

<style scoped>

</style>
