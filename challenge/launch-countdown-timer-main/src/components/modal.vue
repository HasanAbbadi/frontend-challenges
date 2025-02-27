<template>
  <dialog class="modal" ref="dialog">
    <div class="modal__header">
      <h2>Rules</h2>
      <button class="close-modal" @click="closeModal">
        <img src="src/assets/images/icon-close.svg" alt="close" />
      </button>
    </div>
    <div class="modal__content">
      <img src="src/assets/images/image-rules.svg" alt="rules" />
    </div>
  </dialog>
</template>

<script setup>
import { ref } from "vue";

const isOpen = ref(false);
const dialog = ref(null);

const openModal = () => {
  isOpen.value = true;
  dialog.value.showModal();
};

const closeModal = () => {
  isOpen.value = false;
  dialog.value.close();
};

defineExpose({
  openModal,
  closeModal,
});
</script>

<style>
.modal {
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 2rem;
  border-radius: 1rem;
  border: none;
  background-color: var(--clr-fg);
  color: var(--clr-dark-text);
  z-index: 100;
}

.modal::backdrop {
  background-color: rgba(0, 0, 0, 0.5);
}

.modal__header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 2rem;
}

.close-modal {
  background-color: transparent;
  border: none;
  cursor: pointer;
}

.modal__content {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
