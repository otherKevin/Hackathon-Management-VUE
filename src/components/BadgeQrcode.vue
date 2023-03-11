<template>
  <div class="card text-bg-light mb-12" id="qrcode" style="max-width: 32rem">
    <div class="card-header h1">Badge</div>
    <div class="card-body">
      <h5 class="card-title h3">{{ user.firstname }} {{ user.lastname }}</h5>
      <p class="card-text h4">Email: {{ user.email }}</p>
      <form>
        <input type="hidden" v-model="currentUrl" />
      </form>
      <qrcode-vue
        v-if="currentUrl"
        :value="currentUrl"
        :size="size"
        level="H"
      />
    </div>
  </div>
</template>

<script>
import QrcodeVue from "qrcode.vue";

export default {
  beforeMount() {
    this.currentUrl = localStorage.getItem("@currentUrl");
  },
  mounted() {
    this.getUser();
  },

  components: {
    QrcodeVue,
  },
  data() {
    return {
      user: [],
      currentUrl: "",
    };
  },

  props: {
    token: String,
  },

  methods: {
    async getUser() {
      const response = await fetch("http://127.0.0.1:8000/api/my-profile/", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          Authorization: `Bearer ${localStorage.getItem("savedUserToken")}`,
        },
      });

      const data = await response.json();
      this.user = data.user;
    },
  },
};
</script>

<style scoped>
.card {
  border: 2px solid red;
  margin-left: 26rem;
  margin-top: 10rem;
  margin-bottom: 10rem;
}
</style>
