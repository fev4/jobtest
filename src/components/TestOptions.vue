<script setup lang="ts">
import CryptoJS from 'crypto-js';
import { inject, ref, computed } from 'vue'
import Modal from './Modal.vue'
import * as RudderStack from 'rudder-sdk-js';

const name = ref("");
const email = ref("");
const phone = ref("");
const choice = ref("");
const hashedEmail = computed(() => CryptoJS.SHA256(email.value).toString());
const showModal = ref(false)

const rsanalytics = inject('rsanalytics') as typeof RudderStack;

const onSubmit = () => {
  if (rsanalytics) {
    const userTraits = {
      name: name.value,
      email: email.value,
      phone: phone.value,
      choice: choice.value
    }
    rsanalytics.identify(hashedEmail.value, userTraits);
  }
  showModal.value = false
}


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
    <modal :show="showModal" @submit="onSubmit" @close="showModal = false">
      <template #header>
        <h3>custom header</h3>
      </template>
      <template #body>
        <input required type="text" placeholder="Jane Doe" v-model="name">
        <input required type="email" placeholder="jane.doe@email.com" v-model="email">
        <input required type="phone" placeholder="+1 8888888888" v-model="phone">
        <input type="radio" id="option1" value="Job Test 1" v-model="choice">
        <label for="option1">Test One</label>
        <input type="radio" id="option2" value="Job Test 2" v-model="choice">
        <label for="option2">Test Two</label>
      </template>
    </modal>
  </Teleport>
</template>

<style scoped></style>