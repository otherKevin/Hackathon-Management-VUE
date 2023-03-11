<template>
  <hr />
  <div>
    <Admin />
  </div>
</template>

<script>
import Admin from "@/components/Admin.vue";
export default {
  data() {
    return {};
  },
  components: {
    Admin,
  },
  methods: {
    /* Récupération des données de l'event unique sur lequel on se trouve */
    async getEventUnique() {
      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" + this.$route.params.event_id,
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        }
      );
      const data = await response.json();
      this.event = data.event;
    },
  },
};
</script>

<style scoped>
h1,
h2,
table {
  color: rgb(86, 82, 82);
}
form {
  display: flex;
  flex-direction: row;
  flex-wrap: nowrap;
  align-content: center;
  justify-content: center;
  align-items: stretch;
}

button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  height: 30px;
  width: 90px;
  cursor: pointer;
  padding: 10px;
  font-size: 20px;
  display: inline-flex;
  align-content: center;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}
</style>
