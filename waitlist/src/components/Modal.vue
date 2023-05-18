<template>
  <dialog id="modal">
    <div class="close"><Close @click="close" /></div>
    <h1 class="modal-title">We've added you to our waiting list!</h1>
    <div class="modal-sub-title">
      We'll let your Know when <span style="color: #ffffff">dezine.page</span> is ready
    </div>
    <Input
      iconName="email"
      id="email"
      inputType="email"
      placeholder="Enter you email"
      :disabled="false"
    />
  </dialog>
</template>

<script>
import Close from './icons/Close.vue'
import Input from './Input.vue'
import { closeModal } from '../utils/modalFunctions'
export default {
  components: {
    Close,
    Input
  },
  methods: {
    close() {
      closeModal('modal')
    }
  }
}
</script>

<style scoped>
/* #modal {
  background-image: ;
} */

.close {
  display: flex;
  flex-direction: row-reverse;
}

.modal-sub-title {
  width: 19ch;
  margin-top: 2rem;
  margin-bottom: 2rem;
  font-style: normal;
  font-weight: 500;
  font-size: 1rem;
  line-height: 24px;
  color: #667085;
}

dialog {
  padding: 1.5rem;
  box-shadow: 1px 1px 15px rgb(54, 54, 54);
  border: none !important;
  background: #07080c;
  border-radius: 20px;
  max-width: 400px;
}

dialog::backdrop {
  background: rgba(0, 0, 0, 0.6);
}

@media screen and (max-width: 460px) {
  dialog {
    max-width: 360px;
  }
}

@media screen and (max-width: 370px) {
  dialog {
    max-width: 320px;
  }
}

@media screen and (max-width: 320px) {
  dialog {
    max-width: 30px;
  }
}
</style>
