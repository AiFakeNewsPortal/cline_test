<template>
  <div>
    <button @click="toggleScanner">
      {{ buttonText }} QR Scanner
    </button>
    <QrScanner v-if="showScanner" />
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue';
import QrScanner from './QrCodeScanner.vue'; 

const showScanner = ref(false);

function toggleScanner() {
  showScanner.value = !showScanner.value;
}

const buttonText = computed(() => showScanner.value ? 'Hide' : 'Show');
</script>

<style scoped>
/* Add any styles you need here */
</style>