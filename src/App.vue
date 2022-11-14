<template>
  <div class="flex flex-col min-h-screen font-Roboto bg-weather-primary">
    <SiteNavigation />
    <routerView v-slot="{ Component }">
      <Transition name="page" mode="out-in">
        <Component :is="Component" />
      </Transition>
    </routerView>
    <footer class="flex flex-1 items-center justify-center text-white">
      Made with .<i class="fa-regular fa-heart"></i>. by Farhan Agigi
    </footer>
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { RouterView } from "vue-router";
import SiteNavigation from "./components/SiteNavigation.vue";

export default defineComponent({
  name: "App",
  components: {
    SiteNavigation,
  },
});
</script>

<style>
.page-enter-active,
.page-leave-active {
  transition: 600ms ease all;
}

.page-enter-from,
.page-leave-to {
  opacity: 0;
}
</style>
