<script setup lang="ts">
import Modal from './Modal.vue'
import { ref } from 'vue'

const showModal = ref(false)
</script>
<template>
  <div class="g_s-two-columns">
    <div class="g_ctnr">
      <div class="w-layout-grid g_s-two-columns-wrap">
        <div id="w-node-_17c330e1-9b45-28f0-3bf6-6f693d8d15ce-6be41dc2" class="g_s-two-columns-right">
          <div class="g_s-two-columns-title">
            <div class="g_s-two-columns-heading">
              <h2>20 minutes to define your next 20 years.</h2>
            </div>
            <div class="g_s-two-columns-heading-special">
              <h2 class="g_a-h2-special">to define your next 20 years.</h2>
            </div>
          </div>
          <p class="g_a-text-medium">Find answers to:</p>
          <div class="g_s-two-columns-checklist">
            <div class="g_s-two-columns-checklist-item"><img
                src="https://global-uploads.webflow.com/63b58013b3cc40c26785e355/63d3a0d613fdce175d90be48_check.svg"
                loading="lazy" alt="" class="g_s-two-columns-checklist-item-img" />
              <div class="g_s-two-columns-checklist-item-label">
                <div class="g_a-text-large"><strong>Your Career Personality</strong></div>
              </div>
            </div>
            <div class="g_s-two-columns-checklist-item"><img
                src="https://global-uploads.webflow.com/63b58013b3cc40c26785e355/63d3a0d613fdce175d90be48_check.svg"
                loading="lazy" alt="" class="g_s-two-columns-checklist-item-img" />
              <div class="g_s-two-columns-checklist-item-label">
                <div class="g_a-text-large"><strong>Strengths &amp; Weaknesses</strong></div>
              </div>
            </div>
            <div class="g_s-two-columns-checklist-item"><img
                src="https://global-uploads.webflow.com/63b58013b3cc40c26785e355/63d3a0d613fdce175d90be48_check.svg"
                loading="lazy" alt="" class="g_s-two-columns-checklist-item-img" />
              <div class="g_s-two-columns-checklist-item-label">
                <div class="g_a-text-large"><strong>Income Potential</strong></div>
              </div>
            </div>
            <div class="g_s-two-columns-checklist-item"><img
                src="https://global-uploads.webflow.com/63b58013b3cc40c26785e355/63d3a0d613fdce175d90be48_check.svg"
                loading="lazy" alt="" class="g_s-two-columns-checklist-item-img" />
              <div class="g_s-two-columns-checklist-item-label">
                <div class="g_a-text-large"><strong>Path to Financial Freedom</strong></div>
              </div>
            </div>
          </div>
          <button @click="showModal = true" class="g_s-two-columns-cta">
            <div>START THE TEST</div><img
              src="https://global-uploads.webflow.com/63b58013b3cc40c26785e355/63b58014b3cc40878285e38d_ArrowUpRight Black.svg"
              loading="lazy" alt="" class="g_s-btn-arrow-upright" />
          </button>
        </div>
      </div>
    </div>
  </div>

  <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @close="showModal = false">
      <template #header>
        <h3>custom header</h3>
      </template>
    </modal>
  </Teleport>
</template>

<style scoped></style>