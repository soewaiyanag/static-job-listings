<script setup>
defineProps(["job"]);
</script>

<template>
  <div
    class="relative rounded-md bg-white px-5 shadow-md"
    :class="{ 'border-l-[5px] border-primary': job.featured }"
  >
    <img :src="job.logo" alt="logo" class="-mb-4 w-16 -translate-y-1/2" />
    <div class="space-y-3">
      <div class="flex gap-5">
        <h2 class="font-semibold text-primary">
          {{ job.company }}
        </h2>
        <div class="flex gap-2">
          <span
            v-if="job.new"
            class="inline-block rounded-2xl bg-primary px-2 pt-1 text-sm font-medium text-white"
            >NEW!</span
          >
          <span
            v-if="job.featured"
            class="inline-block rounded-2xl bg-very-dark-grayish-cyan px-2 pt-1 text-sm font-medium text-white"
            >FEATURED</span
          >
        </div>
      </div>
      <h3 class="font-semibold">{{ job.position }}</h3>
      <div class="flex gap-2 text-gray-400">
        <span>{{ job.postedAt }}</span>
        •
        <span>{{ job.contract }}</span>
        •
        <span>{{ job.location }}</span>
      </div>
    </div>
  </div>
</template>
