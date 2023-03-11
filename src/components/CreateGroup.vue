<!--******* ESPACE STAFF *******-->
<template>
  <section>
    <div class="groupe">
      <!-- <h3>Choix de l'évènement:</h3> -->

      <!-- liste des events dans un select  -->
      <!-- <select v-model="selectedEvent_id">
        <option :value="null">Tous les événements</option>
        <option v-for="event in events" :key="event.id" :value="event.id">
          {{ event.name }}
          {{ event.location }}
          {{ event.id }}
        </option>
      </select> -->
      <h3>Nouveau groupe</h3>
      <br />

      <form @submit.prevent="createGroup">
        <p>Nom du groupe :</p>
        <input type="text" name="name" v-model="name" />
        <p>Sujet du groupe :</p>
        <input type="text" name="subject" v-model="subject" />
        <p>Salle :</p>
        <input type="text" name="room" v-model="room" />
        <p>Nombre de personnes :</p>
        <input type="text" name="members" v-model="members" />
        <br />
        <!-- 
          Compétences : LES COMPETENCES NE DOIVENT PAS ÊTRE AJOUTEES
          MANUELLEMENT ICI, MAIS IMPORTEES DANS LE GROUPE AUTOMATIQUEMENT LORS
          DE L'AJOUT D'UN PARTICIPANT
         -->
        <br />
        <div>
          <p>Compétences</p>
          <input type="text" name="abilities" v-model="abilities" />
          <input type="hidden" name="event_id" />
        </div>
        <br />
        <div>
          <input type="submit" value="Créer le groupe" id="button" />
        </div>
      </form>
      <br />
      <p>{{ feedbackMessage }}</p>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      groups: [],
      events: [],
      subject: "",
      name: "",
      room: "",
      members: "",
      abilities: "",
      feedbackMessage: "",
      selectedEvent_id: null,
    };
  },
  props: {
    event_id: Number,
  },

  methods: {
    /* Création d'un groupe */
    async createGroup() {
      console.log(
        "Affichage de données du body : subject = " +
          this.subject +
          " event_id = " +
          this.event_id
      );
      const body = {
        subject: this.subject,
        name: this.name,
        room: this.room,
        members: this.members,
        abilities: this.abilities,
        event_id: this.event_id,
      };

      const response = await fetch("http://127.0.0.1:8000/api/groups", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });

      const data = await response.json();

      this.feedbackMessage = data.message;

      this.$emit("groupCreated");

      this.subject = "";
      this.name = "";
      this.room = "";
      this.members = "";
      this.abilities = "";
    },

    /* Récupération des events */
    /* async getEvents() {
      const response = await fetch("http://127.0.0.1:8000/api/events", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      });
      const data = await response.json();
      this.events = data.events;
    }, */

    /* async getGroup() {
      const response = await fetch(
        "http://127.0.0.1:8000/api/groups/" + this.selectedEvent_id,
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        }
      );

      const data = await response.json();
      this.groups = data.groups;
    }, */
    /* watch: {
      selectedEvent_id(id) {
        if (id === null) {
          this.getEvents();
        } else {
          this.getGroup();
        }
      },
    }, */
  },
};
</script>

<style scoped>
h1,
p {
  color: rgb(86, 82, 82);
  font-weight: bold;
}

#button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  cursor: pointer;
  padding: 10px;
  font-size: 16px;
  display: inline-flex;
  align-content: center;
  align-items: center;
  justify-content: center;
  margin-left: 10px;
}

#button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}

li {
  list-style-type: none;
}
</style>
