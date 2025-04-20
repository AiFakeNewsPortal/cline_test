<template>
    <div>
      <button @click="showScanner = !showScanner">
        {{ showScanner ? 'Hide' : 'Show' }} QR Scanner
      </button>
      <QrScanner v-if="showScanner" />
    </div>
  </template>
  
  <script>
  import QrScanner from '~/components/QrScanner.vue'
  
  export default {
    components: {
      QrScanner
    },
    data() {
      return {
        showScanner: false
      }
    }
  }
  </script>
  
  <style scoped>
  /* Add any styles you need here */
  </style>
  