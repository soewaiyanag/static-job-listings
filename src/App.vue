<script setup>
import { ref, onMounted, computed } from "vue";
import JobCard from "./components/JobCard.vue";
import BackgroundImage from "./components/BackgroundImage.vue";

const jobs = ref([]);
const tags = ref([]);

async function fetchJobs() {
  try {
    const response = await fetch("/data.json");
    const data = await response.json();
    jobs.value.push(...data);
  } catch (error) {
    console.error(error);
  }
}

onMounted(fetchJobs); // Call the fetchJobs function on component mount

const filteredJobs = computed(() => {
  if (tags.value.length === 0) return jobs.value; // Return all jobs if no tags are selected
  return jobs.value.filter((job) => {
    const jobTags = [job.role, job.level, ...job.languages, ...job.tools];
    return tags.value.every((tag) => jobTags.includes(tag));
  });
});

const addTag = (t) => {
  if (tags.value.includes(t)) return;
  tags.value.push(t);
};

const removeTag = (t) => {
  tags.value = tags.value.filter((tag) => tag !== t);
};

const clearTags = () => {
  tags.value = [];
};
</script>

<template>
  <BackgroundImage />
  <div class="mx-auto my-16 max-w-4xl px-8">
    <!-- Filter tags -->
    <div
      v-show="tags.length"
      class="flex min-h-12 w-full -translate-y-[5.5rem] items-center gap-4 rounded bg-white px-6 py-4 shadow-sm"
    >
      <div class="flex flex-wrap gap-4">
        <div
          v-for="tag in tags"
          :key="tag"
          class="flex min-w-fit items-center gap-2 overflow-hidden rounded bg-light-grayish-cyan-2 pl-2 font-semibold text-primary"
        >
          <span class="font-semibold">{{ tag }}</span>
          <button
            @click="removeTag(tag)"
            class="ml-auto grid h-5 w-5 place-items-center bg-primary p-1 transition-colors hover:bg-very-dark-grayish-cyan"
          >
            <img src="/images/icon-remove.svg" alt="remove" class="w-3" />
          </button>
        </div>
      </div>
      <button
        @click="clearTags"
        class="ml-auto font-semibold text-gray-500 transition-colors hover:text-primary hover:underline"
      >
        Clear
      </button>
    </div>

    <!-- Job List -->
    <div class="grid gap-14">
      <JobCard
        @add-tag="addTag"
        v-if="filteredJobs.length"
        v-for="job in filteredJobs"
        :job="job"
        :key="job.id"
      />
    </div>
  </div>
</template>
