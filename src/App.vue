<script setup lang="ts">
import JobList from "./components/JobList.vue";
</script>

<template>
  <div
    class="h-52 bg-primary bg-[url('/images/bg-header-mobile.svg')] bg-cover bg-no-repeat sm:bg-[url('/images/bg-header-desktop.svg')] sm:bg-cover"
  ></div>
  <div class="mx-auto my-16 max-w-4xl px-8">
    <JobList />
  </div>
</template>
