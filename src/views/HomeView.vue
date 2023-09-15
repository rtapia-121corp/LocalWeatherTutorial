<template>
  <main class="container text-white">
    <div class="pt-4 mb-8 relative">
      <input 
      type="text" 
      placeholder="Search city" 
      v-model="searchQuery"
      @input="getSearchResults"
      class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary 
        focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
      <ul class="absolute bg-weather-secondary 
        text-white w-full shadow-md py-2 px-1 top-[60px]"
        v-if="mapboxSearchResult"
        >
        <p class="py-2" v-if="searchError">Sorry, somthing went wrong, please try again. </p>
        <p class="py-2" v-if="!searchError && mapboxSearchResult.length === 0"> Not result match yor query, try a different term.</p>
        <template v-else>
          <li v-for="searchResult in mapboxSearchResult" 
          :key="searchResult.id"
           class="py-2 cursor-pointer"
           @click="previewCity(searchResult)"
          >
          {{ searchResult.name}}, {{searchResult.state }}, {{ searchResult.country }}
          </li>
        </template>
      </ul>
    </div>
    <!-- <EmailForm /> -->
  </main>
</template>

<script setup>
import {ref} from "vue";
import axios from "axios";
import { useRouter } from "vue-router";
// import EmailForm from "@/components/EmailForm.vue";

const key = "4ebb4fe1c25ae1433820a605dd9cee2c";
const searchQuery = ref("");
const queryTimeout = ref(null);
const mapboxSearchResult = ref(null);
const searchError = ref(false);

const router = useRouter();
const previewCity = (searchResult) => {
  const city = searchResult.name, state = searchResult.state;
  router.push({
    name: 'city',
    params: {state: state, city: city},
    query: {
      lat: searchResult.lat,
      lon: searchResult.lon,
      preview: true
    }
  });
}

const getSearchResults= () => {
  clearTimeout(queryTimeout.value);
  queryTimeout.value = setTimeout(async () => {
    try{
      if(searchQuery.value !== ''){
      const result = await axios.get(`      http://api.openweathermap.org/geo/1.0/direct?q=${searchQuery.value}&limit=10&appid=${key}`);
      mapboxSearchResult.value=result.data;
      return;
    }
    mapboxSearchResult.value=null;
    }catch{
      searchError.value = true;
    }
    
  },300);  
}
</script>
