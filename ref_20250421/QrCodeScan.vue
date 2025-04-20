<template>
    <div>
      <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>
      <p v-if="decodedContent">Scanned Content: {{ decodedContent }}</p>
      <button v-if="error" @click="retryInitialization">Retry</button>
    </div>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue';
  import { QrcodeStream } from 'vue-qrcode-reader';
  
  const decodedContent = ref<string | null>(null);
  const error = ref<Error | null>(null);
  
  function onDecode(content: string) {
    decodedContent.value = content;
  }
  
  function onInit(promise: Promise<void>) {
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
    // Restart the QR code stream
    const qrcodeStream = document.querySelector('qrcode-stream');
    if (qrcodeStream) {
      qrcodeStream.stop();
      qrcodeStream.start();
    }
  }
  </script>
  
  <style scoped>
  /* Add any styles you need here */
  </style>
  