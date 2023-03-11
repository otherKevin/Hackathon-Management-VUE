<template>
  <section>
    <h1>Mon espace administrateur</h1>
    <br />
    <div class="allPageEvent">
      <div class="createEvent">
        <CreateEvents @created="getEvents" />
        <div class="modify">
          <ModifyEvents
            :name="eventUnique.name"
            :start="eventUnique.start"
            :end="eventUnique.end"
            :location="eventUnique.location"
            :event_id="eventUnique.id"
            @eventModified="getEventUnique"
          />
        </div>
      </div>

      <div class="eventChoiceAndTableUsers">
        <h3>Choix de l'évènement:</h3>

        <!-- liste des events dans un select  -->
        <select v-model="selectedEvent_id">
          <option :value="null">Tous les événements</option>
          <option v-for="event in events" :key="event.id" :value="event.id">
            {{ event.name }}
            {{ event.location }}
            {{ event.id }}
          </option>
        </select>

        <!-- {{ selectedEvent_id }} -->

        <!-- ICI LA LISTE DE TOUS LES UTILISATEURS -->
        <div class="filteredUsers">
          <br />
          <h3>Liste de tous les utilisateurs</h3>
          <br />
          <label for="">Recherche de participant : </label>
          <input
            type="text"
            v-model="searchTerm"
            class=""
            placeholder="Entrez un participant"
          />
          <div class="tableau">
            <table>
              <thead>
                <tr>
                  <th>Utilisateurs</th>
                </tr>
              </thead>
              <tbody>
                <tr>
                  <td class="td">Prénom</td>
                  <td class="td">Nom</td>
                  <td class="td">Email</td>
                  <td class="td">Role</td>
                  <td class="td">Autorisatiton</td>
                </tr>

                <tr v-for="user in filterByName" :key="user.id">
                  <td>{{ user.firstname }}</td>
                  <td>{{ user.lastname }}</td>
                  <td>{{ user.email }}</td>
                  <td></td>
                  <td>
                    <div v-if="selectedEvent_id != null">
                      <select
                        v-model="user.role.Authorization"
                        @change="updateRole(user.role)"
                      >
                        <option value="none">Select</option>
                        <option value="3">Admin - 3</option>
                        <option value="2">Staff - 2</option>
                        <option value="1">User - 1</option>
                      </select>
                    </div>
                  </td>
                </tr>
              </tbody>
            </table>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
import CreateEvents from "@/components/CreateEvents.vue";
import ModifyEvents from "@/components/ModifyEvents.vue";

export default {
  data() {
    return {
      users: [],
      searchTerm: "",
      events: [],
      eventUnique: [],
      selectedEvent_id: null,
      seclectRole_id: null,
    };
  },
  components: {
    CreateEvents,
    ModifyEvents,
  },

  beforeMount() {
    this.getEvents();
    this.getUsers();
  },

  computed: {
    filterByName() {
      return this.users.filter((user) => {
        return (
          user.firstname
            .toLowerCase()
            .includes(this.searchTerm.toLowerCase()) ||
          user.lastname.toLowerCase().includes(this.searchTerm.toLowerCase())
        );
      });
    },
  },

  watch: {
    selectedEvent_id(id) {
      if (id === null) {
        this.getUsers();
      } else {
        this.getUsersOfEvents();
      }
    },
  },

  methods: {
    /* Recherche de tous les utilisateurs inscrits */
    async getUsers() {
      const response = await fetch("http://127.0.0.1:8000/api/showusers", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      });
      const data = await response.json();
      this.users = data.users;
    },

    /* Recherche de tous les utilisateurs inscrits dans un événement */
    async getUsersOfEvents() {
      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" + this.selectedEvent_id,
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        }
      );
      const data = await response.json();
      this.eventUnique = data.event;
      this.users = data.users;
    },

    /* Récupération des events */
    async getEvents() {
      const response = await fetch("http://127.0.0.1:8000/api/events", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      });
      const data = await response.json();
      this.events = data.events;
    },

    /* AUTHORIZATION D UN USER */
    async authorization() {
      const body = {
        title: this.title,
      };

      const response = await fetch("http://127.0.0.1:8000/api/slots", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });

      const data = await response.json();

      this.feedbackMessage = data.message;

      this.getSlots();
    },
  },
};
</script>

<style scoped>
h1,
h2,
h3,
td,
table {
  color: rgb(86, 82, 82);
}

table,
.td {
  border: 1px solid #333;
}

thead {
  background-color: rgb(219, 117, 117);
  color: #fff;
}

.tableau {
  display: flex;
  justify-content: center;
  margin-top: 2%;
  margin-bottom: 5%;
}

.allPageEvent {
  display: flex;
  justify-content: center;
  gap: 6%;
}

.eventChoiceAndTableUsers {
  display: flex;
  flex-direction: column;
}

.filteredUsers {
  margin-top: 4em;
}

.createEvent {
  display: flex;
  flex-direction: column;
}

.modify {
  margin-top: 10%;
}
</style>
