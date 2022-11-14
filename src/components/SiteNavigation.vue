<template>
  <header class="sticky top-0 bg-weather-primary shadow-lg">
    <nav
      class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6"
    >
      <RouterLink :to="{ name: 'home' }">
        <div class="flex items-center gap-3">
          <i class="fa fa-sun text-2xl"></i>
          <p class="text-2xl">The local Weather</p>
        </div>
      </RouterLink>

      <div class="flex gap-3 flex-1 justify-end">
        <span @click="toogleModal">
          <i
            class="fa-solid fa-circle-info text-xl hover:text-weather-secondary duration-150 cursor-pointer"
          ></i>
        </span>
        <!-- @click="toogleModel"></i> -->
        <span @click="addCity" v-if="route.query.preview">
          <i
            class="fa-solid fa-plus text-xl hover:text-weather-secondary duration-150 cursor-pointer"
          ></i>
        </span>
      </div>

      <BaseModel @close-modal="toogleModal" :modalActive="modalActive">
        <div class="text-black">
          <h1 class="text-2xl mb-1">About:</h1>
          <p class="mb-4">
            The local Weather allow you to track the current and future Weather
            of cities of your chosing
          </p>
          <h1 class="text-2xl mb-1">How it works:</h1>
          <ol class="list-decimal list-inside mb-4">
            <li>
              Search for your city by entering the name into the seacrh bar.
            </li>
            <li>
              Select a city within the results, this will take you to the
              current weather for your selection.
            </li>
            <li>
              Track the city bu clicking on the '+' icon in the top right. This
              will save the city to view at a later time on the home page.
            </li>
          </ol>
          <h1 class="text-2xl mb-2">Removing the city</h1>
          <p>
            If you no longer wish to track a city, simply select the city within
            the home page. At the bottom of the page, there will be an option to
            delete city.
          </p>
        </div>
      </BaseModel>
    </nav>
  </header>
</template>

<script setup>
import { defineComponent } from "vue";
import { RouterLink, useRoute, useRouter } from "vue-router";
import BaseModel from "./BaseModel.vue";
import { ref } from "vue";
import { uid } from "uid";

const modalActive = ref(null);
const toogleModal = () => {
  modalActive.value = !modalActive.value;
};

const savedCities = ref([]);
const route = useRoute();
const router = useRouter();
const addCity = () => {
  if (localStorage.getItem("savedCities")) {
    savedCities.value = JSON.parse(localStorage.getItem("savedcities"));
  }

  const locationObj = {
    id: uid(),
    state: route.params.state,
    city: route.params.city,
    coords: {
      lat: route.query.lat,
      lng: route.query.lng,
    },
  };

  savedCities.value.push(locationObj);
  localStorage.setItem("savedCities", JSON.stringify(savedCities.value));

  let query = Object.assign({}, route.query);
  delete query.preview;
  query.id = locationObj.id;
  router.replace({ query });
};
</script>

<style scoped></style>
