<template>
  <h3>Contact:</h3>
  <form @submit.prevent="sendForm">
    <BasicInput v-model="event.name" label="Name" type="text" />
    <BasicInput v-model="event.email" label="E-Mail" type="email" />
    <span v-if="emailError" style="color: red;">{{ emailError }}</span>
    <BasicInput v-model="event.message" label="Message" type="text" />
    <span v-if="messageError" style="color: red;">{{ messageError }}</span>
    <button type="submit">SUBMIT</button>
  </form>
</template>

<script setup>
import BasicInput from "@/components/BasicInput.vue";
import axios from "axios";

const validateEmail = (email) => {
  const regex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
  return regex.test(email);
};
</script>

<script>
import axios from "axios";

export default {
  data() {
    return {
      event: {
        name: "",
        email: "",
        message: ""
      },
      emailError: "",
      messageError: ""
    };
  },
  methods: {
    sendForm() {
      this.emailError = "";
      this.messageError = "";

      if (!validateEmail(this.event.email)) {
        this.emailError = "Please enter a valid email address.";
        return;
      }

      if (this.event.message.trim() === "") {
        this.messageError = "Please enter a message.";
        return;
      }

      axios.post('https://my-json-server.typicode.com/ColaXin/vue3/db.json')
    }
  }
};
</script>
