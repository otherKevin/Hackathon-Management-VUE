<template>
  <div id="container">
    <div class=""><BadgeQrcode :token="this.token" /></div>
  </div>
</template>

<script>
import MyProfile from "@/components/MyProfile.vue";
import BadgeQrcode from "@/components/BadgeQrcode.vue";

export default {
  data() {
    return {
      token: localStorage.getItem("savedUserToken"),
    };
  },

  components: {
    BadgeQrcode,
  },
};
</script>

<style scoped>
h1 {
  color: rgb(86, 82, 82);
}
#container {
  height: 100%;
  margin-bottom: 150px;
}
</style>
