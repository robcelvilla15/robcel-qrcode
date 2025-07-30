<template>
  <v-container class="fill-height" fluid>
    <v-row align="center" justify="center">
      <v-col cols="12" md="8">
        <v-card class="pa-5" elevation="4">
          <v-card-title class="text-h6 text-center">
            <v-icon class="mr-2">mdi-qrcode-scan</v-icon>
            Scan QR Code (Auto UI)
          </v-card-title>
          <v-card-text>
            <!-- Scanner will auto-render here -->
            <div id="reader" style="width: 100%; max-width: 500px; margin: auto;"></div>

            <!-- Scan result output -->
            <v-alert
              v-if="result"
              type="success"
              class="mt-4"
              border="start"
              prominent
            >
              <strong>Result:</strong><br />
              {{ result }}
            </v-alert>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script setup>
import { ref, onMounted, onBeforeUnmount } from 'vue'
import { Html5QrcodeScanner } from 'html5-qrcode'

const result = ref('')
let scannerInstance = null

onMounted(() => {
  scannerInstance = new Html5QrcodeScanner(
    'reader',
    {
      fps: 10,
      qrbox: { width: 250, height: 250 },
      rememberLastUsedCamera: true,
      showTorchButtonIfSupported: true
    },
    false // Set to true for verbose logging
  )

  scannerInstance.render(
    (decodedText) => {
      result.value = decodedText
      scannerInstance.clear()
    },
    (error) => {
      // Optionally log errors
      // console.warn(error)
    }
  )
})

onBeforeUnmount(() => {
  if (scannerInstance) {
    scannerInstance.clear().catch(err => {
      console.warn("Failed to clear scanner on unmount", err)
    })
  }
})
</script>