<template>
  <h3>Contact:</h3>
  <form @submit.prevent="sendForm">
    <BasicInput v-model="store.name" label="Name" type="text" />
    <BasicInput v-model="store.email" label="E-Mail" type="email" />
    <span v-if="emailError" style="color: red;">{{ emailError }}</span>
    <BasicInput v-model="event.message" label="Message" type="text" />
    <span v-if="messageError" style="color: red;">{{ messageError }}</span>
    <button type="submit">SUBMIT</button>
  </form>
</template>

<script setup>
import BasicInput from "@/components/BasicInput.vue";

</script>


<script>


import {useFormStore} from "@/stores/FormStore.js";

export default {
  data() {
    return {
      event: {
        name: "",
        email: "",
        message: ""
      },
      emailError: "",
      messageError: "",
      store: useFormStore()

    };
  },
  methods: {
    async sendForm() {
      this.emailError = "";
      this.messageError = "";

      function validateEmail(email) {
        const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
        return regex.test(email);
      }

      if (!validateEmail(this.store.email)) {
        this.emailError = "Please enter a valid email address.";
        return;
      }

      if (this.event.message.trim() === "") {
        this.messageError = "Please enter a message.";
        return;
      }


      const formData = {
        name: this.store.name,
        email: this.store.email,
        message: this.event.message
      };

      const response = await fetch('http://localhost:3000/formData', {
        method: "POST",
        headers: {
          "Content-Type": "application/json"
        },
        body: JSON.stringify(formData)
      });
      if (response.ok) {
        // If response is successful, show success message
        alert("Form submitted successfully!");
      } else {
        // If response is not successful, show error message
        alert("Failed to submit form. Please try again later.");
      }
    }

  }
};
</script>
