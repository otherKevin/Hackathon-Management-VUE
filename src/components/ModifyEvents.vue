<template>
  <div>
    <h3 class="linkTitlePage">Modification de l'évènement:</h3>
    <!-- Bouton d'affichage du formulaire de modification d'événement -->
    <button @click="revealModifyForm">+</button>
    <div v-if="showModifyForm" id="container">
      <form @submit.prevent="modifyEvent">
        <div>
          <label for="name">Nom:</label>
          <br />
          <input type="text" name="name" v-model="name" />
        </div>

        <br />

        <div>
          <label for="start">Date et heure de début:</label>
          <br />
          <input type="datetime-local" name="start" v-model="start" />
        </div>

        <br />

        <div>
          <label for="end">Date et heure de fin:</label>
          <br />
          <input type="datetime-local" name="end" v-model="end" />
        </div>

        <br />

        <div>
          <label for="location">Lieu:</label>
          <br />
          <input type="text" name="location" v-model="location" />
        </div>

        <br />

        <input type="submit" class="button" value="Modifier" />
      </form>

      <p>{{ feedbackMessage }}</p>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      feedbackMessage: "",
      showModifyForm: false,
      //   token: localStorage.getItem("savedUserToken"),
    };
  },

  props: {
    event_id: Number,
    name: String,
    start: String,
    end: String,
    location: String,
  },

  methods: {
    /* Affichage du formulaire de modification d'événement */
    revealModifyForm() {
      if (this.showModifyForm == false) {
        this.showModifyForm = true;
      } else {
        this.showModifyForm = false;
      }
    },
    /* Modification d'un event */
    async modifyEvent() {
      const body = {
        name: this.name,
        start: this.start,
        end: this.end,
        location: this.location,
      };

      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" + this.event_id,
        {
          method: "PUT",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
            //   Authorization: `Bearer ${localStorage.getItem("savedUserToken")}`,
          },
          body: JSON.stringify(body),
        }
      );
      const data = await response.json();

      this.feedbackMessage = data.message;

      this.name = "";
      this.start = "";
      this.end = "";
      this.location = "";

      this.$emit("eventModified");
    },
  },
};
</script>

<style scoped>
li {
  list-style-type: none;
}

.button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  cursor: pointer;
  padding: 10px;
  font-size: 16px;
  margin-left: 10px;
}

.button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}
h3 {
  color: rgb(86, 82, 82);
}
</style>
