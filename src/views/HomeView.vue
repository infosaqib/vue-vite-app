<script setup>

import Hero from "@/components/Hero.vue";
import Home from "@/components/HomeCards.vue";
import JobListings from "@/components/JobListings.vue";
</script>

<template>
  <Hero title = 'Test title' subtitle="Test subtitle"/>
  <Home />
  <JobListings :limit="5" :showBtn="true"/>
</template>
