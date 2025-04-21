<template>
  <div>
    <button @click="toggleScanner">{{ scannerActive ? 'Stop Scanner' : 'Start Scanner' }}</button>
    <vue3-barcode-qrcode-reader
      v-if="scannerActive"
      @decode="onDecode"
      @error="onError"
    />
    <div v-if="decodedText">
      <p>Decoded Text: {{ decodedText }}</p>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';
import VueBarcodeQrcodeReader from 'vue3-barcode-qrcode-reader';

export default defineComponent({
  components: {
    VueBarcodeQrcodeReader
  },
  setup() {
    const decodedText = ref<string | null>(null);
    const scannerActive = ref<boolean>(false);

    const onDecode = (text: string) => {
      decodedText.value = text;
    };

    const onError = (error: Error) => {
      console.error(error);
    };

    const toggleScanner = () => {
      scannerActive.value = !scannerActive.value;
    };

    return {
      decodedText,
      scannerActive,
      onDecode,
      onError,
      toggleScanner
    };
  }
});
</script>

<style scoped>
/* Add any styles you need here */
</style>
