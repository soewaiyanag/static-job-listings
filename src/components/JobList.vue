<script setup>
import { reactive, onMounted } from "vue";
import JobListItem from "./JobListItem.vue";

const jobs = reactive([]);

async function fetchJobs() {
  try {
    const response = await fetch("/data.json");
    const data = await response.json();
    jobs.push(...data);
  } catch (error) {
    console.error(error);
  }
}

onMounted(fetchJobs); // Call the fetchJobs function on component mount
</script>

<template>
  <div class="grid gap-14">
    <JobListItem v-for="job in jobs" :job="job" :key="job.id" />
  </div>
</template>
