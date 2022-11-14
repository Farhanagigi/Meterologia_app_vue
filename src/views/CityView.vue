<template>
  <div>
    <Suspense>
      <AsyncCityView />
      <template #fallback>
        <CityViewSkeleton />
        <!-- <p>Loading..</p> -->
      </template>
    </Suspense>
  </div>
</template>

<script setup>
import AsyncCityView from "../components/AsyncCityView.vue";
import CityViewSkeleton from "../components/CityViewSkeleton.vue";
</script>
