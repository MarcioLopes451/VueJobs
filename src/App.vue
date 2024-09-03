<script setup>
import Navbar from "./components/Navbar.vue";
import Hero from "./components/Hero.vue";
import HomeCards from "./components/HomeCards.vue";
import JobListings from "./components/JobListings.vue";
</script>

<template>
  <Navbar />
  <Hero title="Test Title" subtitle="test subtitle" />
  <HomeCards />
  <JobListings :limit="4" :showButton="true" />
</template>
