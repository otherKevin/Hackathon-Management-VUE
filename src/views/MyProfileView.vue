<template>
  <div class=""><MyProfile :token="this.token" /></div>
</template>

<script>
import MyProfile from "@/components/MyProfile.vue";

export default {
  data() {
    return {
      token: localStorage.getItem("savedUserToken"),
    };
  },

  components: {
    MyProfile,
  },
};
</script>

<style scoped></style>
