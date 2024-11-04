<script setup>

import Hero from '@/components/Hero.vue';
import Homecards from '@/components/Homecards.vue';
import Joblistings from '@/components/Joblistings.vue';
import { RouterLink } from 'vue-router';
</script>

<template>
  <Hero/>
  <Homecards/>
  <Joblistings :limit="3" :showButton="true"/>
</template>