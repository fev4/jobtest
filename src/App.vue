<script setup lang="ts">
import { provide, readonly } from 'vue';
import TestOptions from './components/TestOptions.vue';
import * as rsanalytics from 'rudder-sdk-js';

rsanalytics.load("2TiqCH4Nq2ylPFjS6UPnSK51EQp", "https://aleeasjobwesgl.dataplane.rudderstack.com");
rsanalytics.page('homepage');

provide('rsanalytics', readonly(rsanalytics));
</script>

<template>
  <TestOptions />
</template>

<style scoped></style>
