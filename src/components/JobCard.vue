<script setup>
import { ref, computed } from "vue";

const { job } = defineProps(["job"]);

const tags = computed(() => {
  const tags = [job.role, job.level, ...job.languages, ...job.tools];
  // Filter out any null or undefined values
  return tags.filter((filter) => filter);
});
</script>

<template>
  <div
    class="relative items-center rounded-md bg-white px-5 pb-5 shadow-md md:flex md:gap-8 md:pt-5"
    :class="{ 'border-l-[5px] border-primary': job.featured }"
  >
    <img
      :src="job.logo"
      alt="logo"
      class="-mb-4 h-14 w-14 -translate-y-1/2 md:mb-0 md:translate-y-0"
    />
    <div
      class="gap-x-6 divide-y divide-neutral-400 md:flex md:w-full md:items-center md:divide-y-0"
    >
      <div class="space-y-3 pb-4 md:pb-0">
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
        <h3
          class="cursor-pointer font-semibold transition-colors hover:text-primary"
        >
          {{ job.position }}
        </h3>
        <div class="flex gap-2 text-gray-400">
          <span class="text-nowrap">{{ job.postedAt }}</span>
          •
          <span class="text-nowrap">{{ job.contract }}</span>
          •
          <span class="text-nowrap">{{ job.location }}</span>
        </div>
      </div>
      <div class="flex flex-wrap gap-4 pt-4 md:ml-auto">
        <button
          v-for="tag in tags"
          @click="$emit('addTag', tag)"
          :key="job.id + tag"
          class="h-min rounded bg-light-grayish-cyan-1 px-2 py-1 font-semibold text-primary transition-colors hover:bg-primary hover:text-white"
        >
          {{ tag }}
        </button>
      </div>
    </div>
  </div>
</template>
