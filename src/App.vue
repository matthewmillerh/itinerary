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
  <div v-if="loggedIn" class="wrapper pl-3 pr-3"> <!-- Password wrapper -->
    <header>
    <div class="flex max-w-3xl ml-auto mr-auto mt-6 bg-gray-200 rounded-lg align-middle">
      <div class="p-5">
        <span class="text-4xl font-bold w-auto">ITINERARY</span>
        <p class="text-sm">24 December, 2024 - 22 January, 2025</p>
      </div>
      <div class="p-5 ml-auto order-2">   
        <p>Emily Rae Smith Labuschagne</p>  
        <div class="border-b-2 border-gray-300 mt-1"></div>  
        <p>Matthew Jason Miller</p>      
      </div>
    </div>
  </header>

  <!-- Content filter bar -->
  <div class="max-w-3xl rounded-lg bg-gray-200 ml-auto mr-auto min-h-12 p-2 mt-3 flex items-center z-20 relative">
    <!-- Countries filter -->
    <div class="min-h-7 flex items-center">
      <button class="text-sm min-h-7 pl-3 pr-3 bg-white rounded-3xl font-semibold hover:bg-gray-400 transition-colors" @click="filterCountries">
        <i class="fa-solid fa-earth-europe" v-if="showCountries === false"></i>
        <i class="fa-solid fa-circle-xmark" v-else></i>
        &nbsp;<span>{{ countryFilterBtn }}</span>
      </button>
    </div>
    <!-- Show Files filter -->
    <div class="text-sm font-semibold min-h-7 flex items-center ml-2 rounded-3xl bg-white pl-3 pr-3">
      Show Files<input class="ml-1" type="checkbox" v-model="showFiles"/>
    </div>
    <!-- Show costs filter -->
    <div class="text-sm font-semibold min-h-7 flex items-center ml-2 mr-2 rounded-3xl bg-white pl-3 pr-3">
      Show Costs<input class="ml-1" type="checkbox" v-model="showCost"/>
    </div>
    <!-- Map view button -->
    <div class="min-h-7 flex items-center ml-auto order-2">
      <button class="text-sm p-1 bg-white rounded-lg font-semibold hover:bg-gray-400 transition-colors" @click="toggleView">
        <i class="fa-solid fa-globe" v-if="!mapView"></i>
        <i class="fa-solid fa-file-lines" v-else></i>
        &nbsp;{{ viewBtnText }}
      </button>
    </div>
    
  </div>
  <!-- Countries filter list -->   
  <div class="max-w-3xl min-h-10 bg-gray-300 -mt-3 rounded-xl ml-auto mr-auto z-0 relative transition-all" v-if="showCountries">
    <div class="flex pt-4 ml-3 items-center flex-wrap">
      <div v-for="country in countries" class="flex items-center">
        <span class="mr-1 text-sm">{{ country }}</span> <input type="checkbox" :id="country" :value="country" class="mr-2" v-model="filteredCountriesList">
    </div>
    </div>
    
  </div>

<!-- Text view wrapper -->
  <div v-if="!mapView">
    <!-- Loop through each day in the itinerary -->
      <!--Day Start-->
      <div v-for="day in data.day">
        <div v-if="filterCountriesList(day.countries)">
          <Itinerary>
            <template v-slot:date>
              <span v-html="day.date"></span>
            </template>  
            <template v-slot:countries>
              <span v-html="day.countries"></span>
            </template>  
          </Itinerary>
          <!-- loop through each item in the day -->
          <div v-for="item in day.items">
            <ItineraryItem :show-files="showFiles" :file-url="item.file" :show-cost="showCost">
              <template v-slot:icon>
                <i v-if="item.type === 'Flight'" class="fa-solid fa-plane"></i>
                <i v-if="item.type === 'Train'" class="fa-solid fa-train"></i>
                <i v-if="item.type === 'Hotel'" class="fa-solid fa-hotel"></i>
                <i v-if="item.type === 'Bus'" class="fa-solid fa-bus"></i>
                <i v-if="item.type === ''" class="fa-regular fa-circle-dot"></i>
              </template>  
              <template #details>
                <span v-html="item.details"></span>
              </template>
              <template #cost>
                {{ item.cost.toLocaleString('en-US', { style: 'currency', currency: 'ZAR' }) }}
              </template>
            </ItineraryItem>
          </div>
        </div>
          
      </div>
      <!--Day End-->
  </div><!-- End Text view wrapper -->

  <!-- Map View wrapper -->
  <div v-else class="max-w-3xl mr-auto ml-auto mt-5">
    <div id="layout" class="max-w-full">
      <Map />
    </div>
  </div><!-- End Map View wrapper -->
  
  
  </div> <!-- End Password Wrapper-->

  <!-- Login Div -->
  <div v-else>
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
