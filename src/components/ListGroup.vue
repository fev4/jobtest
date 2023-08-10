<script setup lang="ts">
import CryptoJS from 'crypto-js';
import { inject, ref, computed } from 'vue'
import Modal from './Modal.vue'
import List from './List.vue';
import * as RudderStack from 'rudder-sdk-js';

const isValidating = ref(false);
const name = ref("");
const email = ref("");
const phone = ref("");
const choice = ref("");
const hashedEmail = computed(() => CryptoJS.SHA256(email.value).toString());
const showModal = ref(false)

const isEmailValid = computed(() => {
  return isValidating.value ? /^[a-zA-Z0-9._%+-]+@[a-zA-Z0-9.-]+\.[a-zA-Z]{2,}$/.test(email.value) : null;
});

const isNameValid = computed(() => {
  return isValidating.value ? name.value.length > 2 : null;
});

const isPhoneValid = computed(() => {
  return isValidating.value ? /^\+?(\d{1,2})?(\s?|\-?|\.?)\(?\d{3}\)?[-.\s]?\d{3}[-.\s]?\d{4}$/.test(phone.value) : null;
})

const isChoiceValid = computed(() => {
  return isValidating.value ? choice.value.length > 0 : null;
})

const rsanalytics = inject('rsanalytics') as typeof RudderStack;

const onSuccessfulSubmission = () => {
  isValidating.value = false;
}

const onSubmit = () => {
  isValidating.value = true;
  if (rsanalytics) {
    const userTraits = {
      name: name.value,
      email: email.value,
      phone: phone.value,
      choice: choice.value
    }
    if (isNameValid.value && isEmailValid.value && isPhoneValid.value && isChoiceValid.value) {
      rsanalytics.identify(hashedEmail.value, userTraits, undefined, onSuccessfulSubmission);
      rsanalytics.track("Form Submission New Lead");
      showModal.value = false
      name.value = "";
      email.value = "";
      phone.value = "";
      choice.value = "";
    }
  }
}

const onOpen = () => {
  showModal.value = true
  if (rsanalytics) {
    rsanalytics.track("Form Submission Opened");
  }
}

const onClose = () => {
  showModal.value = false
  isValidating.value = false;
  name.value = "";
  email.value = "";
  phone.value = "";
  choice.value = "";
  if (rsanalytics) {
    rsanalytics.track("Form Submission Closed");
  }
}


</script>
<template>
  <div class="two-columns">
    <h2 class="two-columns-title">20 minutes to define your next 20 years </h2>
    <div class="w-layout-grid two-columns-wrap">
      <div class="g_s-two-columns-left">
        <List title="Quick and simple" />
      </div>
      <div class="g_s-two-columns-right">
        <List title="In depth & detailed" />
      </div>
    </div>
    <button @click="onOpen" class="btn-large-cyan v-inline-block">
      <span class="btn-content">
        Start now
        <img src="/src/svg/63b58014b3cc40878285e38d_arrowupright_black.svg" loading="lazy" alt=""
          class="g_s-btn-arrow-upright" />
      </span>
    </button>
  </div>

  <Teleport to="body">
    <!-- use the modal component, pass in the prop -->
    <modal :show="showModal" @submit="onSubmit" @close="onClose">
      <template #header>
        <h3>Getting started</h3>
        <p>Get your custom job test right away, simply fill out a few details and we'll contact you.</p>
      </template>
      <template #body>
        <label class="label-large">
          <span :class="{ valid: isNameValid === true, invalid: isNameValid === false }">{{ isNameValid === false ? `The
            name
            must be at least 2 characters long` : `What's
            your name ? * ` }}</span>
          <input type="text" placeholder="Jane Doe" v-model="name">
        </label>
        <label class="label-large">
          <span :class="{ valid: isEmailValid === true, invalid: isEmailValid === false }">{{ isEmailValid === false ?
            `The email must be valid` : `What's your email address? *` }}</span>
          <input type="email" placeholder="jane.doe@email.com" v-model="email">
        </label>
        <label class="label-large">
          <span :class="{ valid: isPhoneValid === true, invalid: isPhoneValid === false }">{{ isPhoneValid === false ?
            `The phone must be 10 digits` : `What's your phone number? *` }}</span>
          <input type="phone" placeholder="+1 8888888888" v-model="phone">
        </label>
        <div class="bold-text">
          <span :class="{ valid: isChoiceValid === true, invalid: isChoiceValid === false }">{{ isChoiceValid === false ?
            `Please select one of the two options` : `What test are you interested in? *` }}</span>
          <div class="checkbox-options">
            <label for="option1">Test One
              <input type="radio" id="option1" value="Job Test 1" v-model="choice">
            </label>
            <label for="option2">Test Two
              <input type="radio" id="option2" value="Job Test 2" v-model="choice">
            </label>
          </div>
        </div>
        <p class="note">* Required fields</p>
      </template>
    </modal>
  </Teleport>
</template>

<style scoped>
.valid {
  color: black;
}

.invalid {
  color: red;
}

.bold-text {
  font-weight: bold;
}

.note {
  font-size: 12px;
  color: #999;
  font-style: italic;
}

.label-large {
  display: flex;
  flex-direction: column;
  padding: 0.3rem 0;
}

.checkbox-options {
  display: flex;
  justify-content: space-between;
  width: 40%;
}

.checkbox-options label {
  gap: 10px;
}

input[type="text"],
input[type="email"],
input[type="phone"] {
  width: 100%;
  border-radius: 10px;
  padding: 0.3rem;
}
</style>