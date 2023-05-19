<template>
  <main class="hdr">
    <div class="main_form">
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
          v-model="name"
          :autofocus="true"
        />
        <Input
          iconName="email"
          id="email"
          inputType="email"
          placeholder="Enter you email"
          v-model="email"
          :disabled="!isNameValid"
        />
        <div>
          <Button @click="postDetails" :disabled="!isEmailValid" :submitting="submitting" />
        </div>
        <div class="error" v-if="formSubmissionFailed">
          There was some issue in submitting the details, we are already looking into it. please try
          again later, do follow our <a href="https://twitter.com/DezinePage/">Twitter</a> handle
          for updates
        </div>
      </div>
    </div>
    <div class="img-holder__illustration">
      <img class="illustration" src="@/assets/images/illustration.webp" alt="illustration" />
    </div>
  </main>
  <Modal :email="previousEmail" />
</template>

<script>
import Input from '@/components/Input.vue'
import Button from '@/components/Button.vue'
import Modal from '@/components/Modal.vue'
import { openModal } from '@/utils/modalFunctions'
import { collection, addDoc, serverTimestamp } from 'firebase/firestore'
import { logEvent } from 'firebase/analytics'
import { db, analytics } from '@/utils/firebase'
import { validateEmail } from '@/utils/helpers'
export default {
  components: {
    Input,
    Button,
    Modal
  },
  data() {
    return {
      collection_name: import.meta.env.VITE_collection_name,
      name: '',
      email: '',
      previousEmail: '',
      isNameValid: false,
      isEmailValid: false,
      submitting: false,
      formSubmissionFailed: false
    }
  },
  methods: {
    getRequestObject() {
      return {
        name: String(this.name),
        email: String(this.email),
        timeStamp: serverTimestamp()
      }
    },
    resetFormData() {
      this.previousEmail = this.email
      this.name = ''
      this.email = ''
    },
    async postDetails() {
      const paylaod = this.getRequestObject()
      this.submitting = true
      try {
        await addDoc(collection(db, this.collection_name), paylaod)
        openModal('modal')
        logEvent(analytics, 'joined_waitlist', { timeStamp: new Date().valueOf() })
        this.resetFormData()
      } catch (e) {
        logEvent(analytics, 'unexpected_error', { timeStamp: new Date().valueOf() })
        this.formSubmissionFailed = true
      } finally {
        this.submitting = false
      }
    }
  },
  watch: {
    name(newName, oldName) {
      const enteredName = String(newName)
      if (enteredName.length > 2) this.isNameValid = true
      else this.isNameValid = false
    },
    email(newEmail, oldEmail) {
      const enteredEmail = String(newEmail)
      if (enteredEmail.length > 2 && validateEmail(enteredEmail)) this.isEmailValid = true
      else this.isEmailValid = false
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
  animation: fadeInRight 0.8s ease-out;
}

.error {
  margin-top: 2rem;
  margin-bottom: 2rem;
  font-style: normal;
  font-weight: 500;
  font-size: 1rem;
  line-height: 24px;
  color: red;
}

.main_form {
  animation: fadeInLeft 0.8s ease-out;
}

/*========== MEDIA QUERIES ==========*/

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
</style>
