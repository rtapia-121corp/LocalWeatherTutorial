<template>
  <main class="container text-white">
    <!-- <div class="pt-4 mb-8 relative">
      <input 
      type="text" 
      placeholder="Search city" 
      class="py-2 px-1 w-full bg-transparent border-b focus:border-weather-secondary 
        focus:outline-none focus:shadow-[0px_1px_0_0_#004E71]"
      />
    </div> -->

    <EmailForm />
  </main>
</template>

<script setup>
import {ref} from "vue";
import axios from "axios";
import EmailForm from "@/components/EmailForm.vue";

const searchQuery = ref("");
const queryTimeout = ref(null);

const getSearchResults= () => {
  queryTimeout.value = setTimeout(async () => {
    if(searchQuery.value !== ''){
      const result = await axios.get();
    }
  },300);  
}
</script>
