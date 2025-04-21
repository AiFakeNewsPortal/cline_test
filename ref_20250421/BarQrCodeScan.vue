<template>
  <div>
    <vue3-barcode-qrcode-reader
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

    const onDecode = (text: string) => {
      decodedText.value = text;
    };

    const onError = (error: Error) => {
      console.error(error);
    };

    return {
      decodedText,
      onDecode,
      onError
    };
  }
});
</script>

<style scoped>
/* Add any styles you need here */
</style>
