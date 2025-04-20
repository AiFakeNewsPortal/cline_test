<template>
    <div>
      <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>
      <p v-if="decodedContent">Scanned Content: {{ decodedContent }}</p>
      <button v-if="error" @click="retryInitialization">Retry</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import { QrcodeStream } from 'vue-qrcode-reader'
  
  const decodedContent = ref(null);
  const error = ref(null);

  function onDecode(content) {
    decodedContent.value = content;
  }

  function onInit(promise) {
    promise.catch(err => {
      if (err.name === 'NotAllowedError') {
        alert('Please allow camera access to scan QR codes.');
      } else {
        alert('An error occurred while initializing the QR scanner.');
      }
      error.value = err;
    });
  }

  function retryInitialization() {
    error.value = null;
    // Assume there is a method to restart the QR code stream
    restartQrCodeStream();
  }
  </script>
  
  <style scoped>
  /* Add any styles you need here */
  </style>