<template>
    <heder class="sticky top-0 bg-weather-primary shadow-lg">
        <nav class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6">
            <RouterLink :to="{ name: 'home' }">
                <div class="flex items-center gap-3 ">
                    <i class="fa-solid fa-sun text-2xl"></i>
                    <p class="text-2xl">The Local Weather</p>
                </div>
            </RouterLink>

            <div class="flex gap-3 flex-1 justify-end">
                <i class="fa-solid fa-circle-info text-xl 
                hover:text-weather-secondary duration-150 cursor-pointer" @click="toggleModal"></i>
                <i class="fa-solid fa-plus text-xl 
                hover:text-weather-secondary duration-150 cursor-pointer"></i>
            </div>

            <BaseModal :modalActive="modalActive"  @close-modal="toggleModal">
                <div class="text-black">
                <h2 class="text-2xl mb-1"> About </h2>
                <p class="mb-4"> 
                    What is Lorem Ipsum?
                    Lorem Ipsum is simply dummy text of the printing and typesetting industry. Lorem Ipsum has been the
                    industry's standard dummy text ever since the 1500s, when an unknown printer took a galley of type and
                    scrambled it to make a type specimen book. It has survived not only five centuries, but also the leap
                    into electronic typesetting, remaining essentially unchanged. It was popularised in the 1960s with the
                    release of Letraset sheets containing Lorem Ipsum passages, and more recently with desktop publishing
                    software like Aldus PageMaker including versions of Lorem Ipsum.
                </p>
                <ol class="list-decimal list-inside mb-4">
                    <li>Element 1</li>
                    <li>Element 2</li>
                    <li>Element 3</li>
                    <li>Element 4</li>
                </ol>
                <h2 class="text-2xl mb-1"> Soon </h2>
                <P class="mb-4">
                    Why do we use it?
                    It is a long established fact that a reader will be distracted by the readable content of a page when
                    looking at its layout. The point of using Lorem Ipsum is that it has a more-or-less normal distribution
                    of letters, as opposed to using 'Content here, content here', making it look like readable English. Many
                    desktop publishing packages and web page editors now use Lorem Ipsum as their default model text, and a
                    search for 'lorem ipsum' will uncover many web sites still in their infancy. Various versions have
                    evolved over the years, sometimes by accident, sometimes on purpose (injected humour and the like).
                </P>
            </div>
            </BaseModal>
        </nav>
</heder></template>

<script setup>
import {ref } from "vue";
import { RouterLink } from "vue-router";
import BaseModal from "./BaseModal.vue"
const modalActive = ref(null);

const toggleModal = () => {
    modalActive.value = !modalActive.value
}
</script>

