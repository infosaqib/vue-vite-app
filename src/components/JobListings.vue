<script setup>
import { reactive, onMounted, ref, computed } from "vue";
import jobListing from "@/components/JobListing.vue";
import axios from "axios";
import PulseLoader from "vue-spinner/src/PulseLoader.vue";

defineProps({
  limit: Number,
  showBtn: {
    type: Boolean,
    default: false,
  },
});

const state = reactive({
  jobs: [],
  isLoading: true,
});

const search = ref();

const filterJobs = computed(() => {
  return state.jobs.filter((job) =>
    job.title.toLowerCase().includes(search.value.toLowerCase()),
  );
});

onMounted(async () => {
  try {
    const res = await axios.get("/api/jobs");
    state.jobs = res.data;
  } catch (error) {
    console.error("Error fetching data: " + error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <section class="bg-green-50 px-4 py-10">
    <div class="container-xl lg:container m-auto">
      <form>
        <input
          v-model="search"
          type="search"
          name=""
          id=""
          placeholder="search"
          @input="filterJobs"
        />
      </form>
      <h2 class="text-3xl font-bold text-green-500 mb-6 text-center">
        Browse Jobs
      </h2>
      <div v-if="state.isLoading" class="text-green-600 text-center py-6">
        <PulseLoader />
      </div>
      <div v-else class="grid grid-cols-1 md:grid-cols-3 gap-6">
        <jobListing
          v-for="job in filterJobs.slice(0, limit || filterJobs.length)"
          :key="job.id"
          :job="job"
        />
      </div>
    </div>
  </section>

  <section class="m-auto max-w-lg my-10 px-6">
    <RouterLink
      v-if="showBtn"
      to="/jobs"
      class="block bg-black text-white text-center py-4 px-6 rounded-xl hover:bg-gray-700"
      >View All Jobs</RouterLink
    >
  </section>
</template>
