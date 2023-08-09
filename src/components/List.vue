<script setup lang="ts">

defineProps({
  items: {
    type: Array,
    default: () => ['Your career personality', 'Strengths & weaknesses', 'Income potential', 'Path to financial freedom']
  },
  title: {
    type: String,
    default: () => 'Test Career A'
  },
  subtitle: {
    type: String,
    default: () => 'Find answers to:'
  }
})
</script>
<template>
  <h3>{{ title }}</h3>
  <p class="g_a-text-medium">{{ subtitle }}</p>
  <div class="g_s-two-columns-checklist">
    <div class="g_s-two-columns-checklist-item" v-for="(item, index) in items" :key="index"><img
        src="/src/svg/63d3a0d613fdce175d90be48_check.svg" loading="lazy" alt=""
        class="g_s-two-columns-checklist-item-img" />
      <div class="g_s-two-columns-checklist-item-label">
        <div class="g_a-text-large"><strong>{{ item }}</strong></div>
      </div>
    </div>
  </div>
</template>

<style scoped></style>