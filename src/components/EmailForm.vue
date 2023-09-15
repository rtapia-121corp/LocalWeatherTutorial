<template>
    <div class="pt-4 m-8 relative">
        <form @submit.prevent="sendEmail" class="from-black">
            <div class="space-y-12  text-white">
                <div class="border-b border-gray-900/10 pb-12">
                    <h2 class="text-base font-semibold leading-7">Profile</h2>
                    <p class="mt-1 text-sm leading-6">This information will be displayed publicly so be careful what you
                        share.</p>
                    <div class="mt-10 grid grid-cols-1 gap-x-6 gap-y-8 sm:grid-cols-6">
                        <div class="sm:col-span-4">
                            <label for="email" class="block text-sm font-medium leading-6">Email address</label>
                            <div class="mt-2">
                                <input id="email" name="email" type="email" autocomplete="email" class="block w-full rounded-md border-0 py-1.5 shadow-sm ring-1 ring-inset ring-gray-300 bg-transparent
                          focus:ring-2 focus:ring-inset focus:ring-weather-secondary sm:text-sm sm:leading-6" />
                            </div>
                        </div>

                        <div class="col-span-full">
                            <label for="promt" class="block text-sm font-medium leading-6">Promt</label>
                            <div class="mt-2">
                                <textarea id="promt" name="promt" rows="3"
                                    class="block w-full rounded-md border-0 py-1.5 shadow-sm ring-1 ring-inset  bg-transparent 
                         ring-gray-300 focus:ring-2 focus:ring-inset focus:ring-weather-secondary  sm:text-sm sm:leading-6" />
                            </div>
                            <p class="mt-3 text-sm leading-6">Write a few sentences promt your idea</p>
                        </div>

                    </div>
                </div>
            </div>
            <div class="mt-6 flex items-center justify-end gap-x-6">
                <button type="submit"
                    class="rounded-md bg-weather-secondary px-8 py-3 text-sm font-semibold text-white shadow-sm hover:bg-weather-secondary 
                     focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-weather-secondary ">Send</button>
            </div>
        </form>
    </div>
</template>

<script setup>
import { ref } from "vue";
import axios from "axios";

const email = ref("");
const promt = ref("");

const sendEmail = () => {
//   queryTimeout.value = setTimeout(async () => {
//     if(email.value !== '' && promt.value !==''){
//         const response = await axios.post('https://localhost:7089/api/Emails/?', {
//           email: email.value,
//           promt: promt.value
//         }).then((response) => {})
//     }
//   },300);

}
</script>

<style lang="scss" scoped></style>