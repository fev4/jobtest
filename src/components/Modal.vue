<script setup lang="ts">
import { onMounted, onUnmounted } from 'vue';

const { show } = defineProps<{ show: Boolean }>()
const emit = defineEmits(['close']);

const closeOnEsc = (event: KeyboardEvent) => {
  if (event.key === 'Escape') {
    emit('close');
  }
};

onMounted(() => {
  window.addEventListener('keydown', closeOnEsc);
});

onUnmounted(() => {
  window.removeEventListener('keydown', closeOnEsc);
});
</script>

<template>
  <Transition name="modal">
    <div v-if="show" class="modal-mask" @click.self="$emit('close')">
      <div class="modal-container">
        <div class="modal-header">
          <slot name="header">default header</slot>
        </div>
        <form>
          <div class="modal-body">
            <slot name="body">default body</slot>
          </div>

          <div class="modal-footer">
            <button class="btn-modal btn-small" @click.prevent="$emit('close')">Cancel</button>
            <button class="btn-modal btn-small-cyan" @click.prevent="$emit('submit')">Submit</button>
          </div>
        </form>
      </div>
    </div>
  </Transition>
</template>

<style>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  transition: opacity 0.3s ease;
}

.modal-container {
  max-width: 550px;
  margin: auto;
  padding: 20px 30px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  border-radius: 10px;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

.modal-enter-from {
  opacity: 0;
}

.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .modal-container,
.modal-leave-to .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.modal-footer {
  display: flex;
  justify-content: space-between;
}

.btn-modal {
  text-align: center;
  letter-spacing: .08em;
  text-transform: uppercase;
  border-radius: 25px;
  justify-content: center;
  align-items: center;
  font-size: 16px;
  font-weight: 700;
  line-height: 32px;
  text-decoration: none;
  display: flex;
  position: relative;
  overflow: hidden;
}

.btn-small {
  transition: all .3s ease-in;
  padding: 10px 20px;
  color: #000;
  background-color: unset;
}

.btn-small:hover {
  background-color: #d2d0d0;
}

.btn-small-cyan {
  transition: all .3s ease-in;
  padding: 10px 20px;
  color: #000;
  background-color: #5bead0;
}

.btn-small-cyan:hover {
  background-color: #d8a4ff;
}
</style>