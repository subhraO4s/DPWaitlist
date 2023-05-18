<template>
  <main class="hdr">
    <div>
      <div class="img-holder__logo">
        <img src="@/assets/images/logo.webp" alt="logo of dezie.page" />
      </div>
      <div class="title">Join the waitlist for building your digital presence.</div>
      <div class="form-area">
        <Input
          iconName="user"
          id="user"
          inputType="text"
          placeholder="Enter you name"
          :disabled="false"
          :autofocus="true"
        />
        <Input
          iconName="email"
          id="email"
          inputType="email"
          placeholder="Enter you email"
          :disabled="false"
        />
        <div>
          <Button @click="open" />
        </div>
      </div>
    </div>
    <div class="img-holder__illustration">
      <img class="illustration" src="@/assets/images/illustration.webp" alt="illustration" />
    </div>
  </main>
  <Modal />
</template>

<script>
import Input from '@/components/Input.vue'
import Button from '@/components/Button.vue'
import Modal from '@/components/Modal.vue'
import { openModal } from '@/utils/modalFunctions'
export default {
  components: {
    Input,
    Button,
    Modal
  },
  methods: {
    open() {
      openModal('modal')
    }
  }
}
</script>

<style scoped>
.form-area {
  padding-top: 1.5rem;
}

.hdr {
  width: 100%;
  align-items: center;
  flex-grow: 1;
  display: grid;
  gap: 1.4rem;
  grid-auto-columns: 1fr;
  grid-template-areas: 'one two';
}

.img-holder__logo {
  padding-bottom: 1rem;
}

.img-holder__illustration {
  display: flex;
  justify-content: center;
  align-items: center;
}

/*========== MEDIA QUERIES ==========*/
@media screen and (min-width: 1024px) {
}

@media screen and (max-width: 960px) {
  .illustration {
    width: calc(var(--illustration-width) * 0.75);
  }
}

@media screen and (max-width: 800px) {
  .hdr {
    gap: 3rem;
    grid-template-areas: 'one';
  }
  .img-holder__logo {
    display: flex;
    justify-content: center;
  }
}

@media screen and (max-width: 460px) {
  .illustration {
    width: calc(var(--illustration-width) * 0.5);
  }
}

@media screen and (max-width: 360px) {
}
</style>
