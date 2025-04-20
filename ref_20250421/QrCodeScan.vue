<template>
    <div>
      <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>
      <p v-if="decodedContent">Scanned Content: {{ decodedContent }}</p>
    </div>
  </template>
  
  <script>
  import { QrcodeStream } from 'vue-qrcode-reader'
  
  export default {
    components: {
      QrcodeStream
    },
    data() {
      return {
        decodedContent: null
      }
    },
    methods: {
      onDecode(content) {
        this.decodedContent = content
      },
      onInit(promise) {
        promise.catch(error => {
          if (error.name === 'NotAllowedError') {
            alert('Please allow camera access to scan QR codes.')
          } else {
            alert('An error occurred while initializing the QR scanner.')
          }
        })
      }
    }
  }
  </script>
  
  <style scoped>
  /* Add any styles you need here */
  </style>
  