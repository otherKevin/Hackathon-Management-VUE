<template>
  <br />
  <div>
    <p>{{ error }}</p>
    <p>{{ decodeString }}</p>
    <qrcode-stream @init="onInit" @decode="onDecode"></qrcode-stream>
  </div>
</template>

<script>
import { QrcodeStream } from "vue3-qrcode-reader";
export default {
  data() {
    return {
      decodeString: "",
    };
  },
  components: {
    QrcodeStream,
  },
  methods: {
    async onInit(promise) {
      try {
        const { capabilities } = await promise;

        // successfully initialized
      } catch (error) {
        if (error.name === "NotAllowedError") {
          this.error = "user denied camera access permisson";
        } else if (error.name === "NotFoundError") {
          this.error = "no suitable camera device installed";
        } else if (error.name === "NotSupportedError") {
          this.error = "page is not served over HTTPS (or localhost)";
        } else if (error.name === "NotReadableError") {
          this.error = "maybe camera is already in use";
        } else if (error.name === "OverconstrainedError") {
          this.error =
            "did you requested the front camera although there is none?";
        } else if (error.name === "StreamApiNotSupportedError") {
          this.error = "browser seems to be lacking features";
        }
      } finally {
        // hide loading indicator
      }
    },
    onDecode(decodeString) {
      this.decodeString = decodeString;
      window.location.replace(decodeString);
    },
  },
};
</script>

<style scoped>
.inputStyle {
  margin-top: 80px;
}

#container {
  height: 100%;
}
</style>
