<template>
  <hr />
  <h1>Evènement {{ name }}</h1>
  <div class="eventDiv">
    <p>Date de début: {{ start }}</p>
    <p>Date de fin: {{ end }}</p>
    <p>Lieu: {{ location }}</p>
    <p>{{ event_id }}</p>

    <div id="styleButton">
      <router-link
        v-if="!viewing"
        :to="{
          name: 'EventUnique',
          params: {
            event_id: this.event_id,
          },
        }"
      >
        <button class="test" @click="showEvent">
          Montrer l'évènement
        </button></router-link
      >

      <button @click="deleteEvent">Supprimer</button>
      <br />
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      message: "",
    };
  },
  props: {
    name: String,
    start: String,
    end: String,
    location: String,
    event_id: Number,
    viewing: Boolean,
  },

  methods: {
    async deleteEvent() {
      console.log(
        "entrée dans méthode delete avec event_id : " + this.event_id
      );
      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" + this.event_id,

        {
          method: "DELETE",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        }
      );

      const data = await response.json();
      this.message = data.message;
      this.$emit("eventDeleted");
      window.location.href = "/#/eventlist";
    },
  },
};
</script>
<style scoped>
h1 {
  color: rgb(86, 82, 82);
}
button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  height: 30px;
  width: 180px;
  cursor: pointer;
  padding: 10px;
  font-size: 16px;
  display: inline-flex;
  align-content: center;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
  margin-right: 10px;
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
  font-size: 0.95em;
}
</style>
