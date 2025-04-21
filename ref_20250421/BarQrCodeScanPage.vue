<template>
  <div>
    <h1>Barcode and QR Code Scanner</h1>
    <BarcodeQRCodeReader />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import BarcodeQRCodeReader from '~/components/BarcodeQRCodeReader.vue';

export default defineComponent({
  components: {
    BarcodeQRCodeReader
  }
});
</script>

<style scoped>
/* Add any styles you need here */
</style>
