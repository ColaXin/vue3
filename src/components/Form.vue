<script setup>

import BasicInput from "@/components/BasicInput.vue";
import axios from "axios";
</script>

<script>
export default {
  data () {
    return {
      event: {
        name: '',
        email: '',
        message: ''
      }
    }
  },
  methods: {
    sendForm () {

    }
  }
}
</script>

<template>

  <h3>Contact: </h3>
 <form @submit.prevent="sendForm">
   <BasicInput
       v-model="event.name"
       label="Title"
       type="text"/>

   <BasicInput
       v-model="event.email"
       label="E-Mail "
       type="text"/>
   <BasicInput
       v-model="event.message"
       label="Message"
       type="text"/>

   <button type="submit">SUBMIT</button>

 </form>
</template>

<style scoped>

.container {
  overflow-y: auto;
  padding: 10px;
  display: flex;
  flex-grow: 1;
  flex-direction: column;
  margin: 5px;
}

.label {
  font-size: 16px;
  font-family: "Arial";
  margin-bottom: 0;
}

.field {
  font-size: 20px;
  font-family: "Arial";
  color: black;
  width: 200px;
  margin-top: 2px;
  margin-bottom: 5px;
}





</style>