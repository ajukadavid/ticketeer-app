<template>
<section>
    <h3>qr scanner component</h3>
    <qrcode-stream @decode="onDecode" @init="onInit"></qrcode-stream>
</section>
</template>

<script setup lang="ts">
import { QrcodeStream } from 'vue-qrcode-reader'
const onDecode = (decondedString:string) => {
    console.log(decondedString)
}
const onInit = async (promise: any) => {
    try {
      const { capabilities } = await promise
      console.log(capabilities)

      // successfully initialized
    } catch (error: any) {
      if (error.name === 'NotAllowedError') {
        // user denied camera access permisson
      } else if (error.name === 'NotFoundError') {
        // no suitable camera device installed
      } else if (error.name === 'NotSupportedError') {
        // page is not served over HTTPS (or localhost)
      } else if (error.name === 'NotReadableError') {
        // maybe camera is already in use
      } else if (error.name === 'OverconstrainedError') {
        // did you requested the front camera although there is none?
      } else if (error.name === 'StreamApiNotSupportedError') {
        // browser seems to be lacking features
      }
    } finally {
      // hide loading indicator
    }
}
</script>

<style scoped>

</style>