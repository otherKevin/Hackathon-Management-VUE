<template>
  <h2>Sélectionnez un événement à gérer :</h2>
  <!-- liste des events dans un select  -->
  <select v-model="selectedEvent_id">
    <option :value="null">Tous les événements</option>
    <option v-for="event in events" :key="event.id" :value="event.id">
      {{ event.name }}
      {{ event.location }}
      {{ event.id }}
    </option>
  </select>
  <hr />
  <div class="componenterinos">
    <div class="col-6">
      <h2>Groupes</h2>
      <hr />
      <!-- Bouton d'affichage du formulaire de création de groupe -->
      <button @click="revealCreateGroupForm">{{ addGroupButton }}</button>
      <CreateGroup
        v-if="showCreateGroupForm"
        :event_id="this.selectedEvent_id"
      />
      <hr />
    </div>
    <div class="col-6">
      <h2>Créneaux</h2>
      <hr />
      <!-- Bouton d'affichage du formulaire de création de groupe -->
      <button @click="revealCreateSlotForm">{{ addSlotButton }}</button>
      <CreateSlots
        v-if="showCreateSlotForm"
        :event_id="this.selectedEvent_id"
      />
      <hr />
    </div>
  </div>
  <hr />
  <!-- En-dessous, en deux colonnes, les groupes et les créneaux liés à l'événement séléctionné -->
  <!-- Disposition propice à la mise en place du "glisser-déposer" des groupes dans les cases de créneaux -->
  <div class="componenterinos">
    <!-- Colonne des groupes -->
    <div v-if="selectedEvent_id != null" class="col-6">
      <h3>Listes des groupes</h3>
      <GroupUnique
        v-for="group in groups"
        :key="group.id"
        :name="group.name"
        :subject="group.subject"
        :room="group.room"
        :members="group.members"
        :abilities="group.abilities"
        :group_id="group.id"
        :event_id="group.event_id"
        :viewing="false"
      />
      <br />
    </div>
    <!-- Colonne des créneaux -->
    <div v-if="selectedEvent_id != null" class="col-6">
      <h3>Listes des créneaux</h3>
      <SlotUnique
        v-for="slot in slots"
        :key="slot.id"
        :title="slot.title"
        :start="slot.start"
        :duration="slot.duration"
        :teams="slot.teams"
        :event_id="slot.event_id"
      />
      <br />
    </div>
  </div>
</template>

<script>
import CreateSlots from "@/components/CreateSlots.vue";
import CreateGroup from "@/components/CreateGroup.vue";
import GroupUnique from "@/components/GroupUnique.vue";
import SlotUnique from "@/components/SlotUnique.vue";

export default {
  components: {
    CreateSlots,
    CreateGroup,
    GroupUnique,
    SlotUnique,
  },
  beforeMount() {
    this.getEvents();
  },

  data() {
    return {
      events: [],
      selectedEvent_id: null,
      showCreateGroupForm: false,
      showCreateSlotForm: false,
      addGroupButton: "+",
      addSlotButton: "+",
      groups: [],
      slots: [],
    };
  },

  watch: {
    selectedEvent_id(id) {
      if (id === null) {
        this.getEvents();
      } else {
        console.log("id d'événement sélectionné");
        this.getGroups();
        //this.getSlots();
      }
    },
  },

  methods: {
    /* Affichage du formulaire de création de groupe */
    revealCreateGroupForm() {
      if (this.showCreateGroupForm == false) {
        this.showCreateGroupForm = true;
        this.addGroupButton = "-";
      } else {
        this.showCreateGroupForm = false;
        this.addGroupButton = "+";
      }
    },
    /* Affichage du formulaire de création de créneau */
    revealCreateSlotForm() {
      if (this.showCreateSlotForm == false) {
        this.showCreateSlotForm = true;
        this.addSlotButton = "-";
      } else {
        this.showCreateSlotForm = false;
        this.addSlotButton = "+";
      }
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

    /* Récupération des groupes en fonction de l'événement séléctionné */
    async getGroups() {
      console.log(
        "entrée dans getGroup avec selectedEvent_id = " + this.selectedEvent_id
      );
      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" + this.selectedEvent_id + "/groups",
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
      console.log("sortie de getGroups avec this.groups = " + this.groups);
    },

    /* Récupération des slots en fonction de l'événement séléctionné */
    async getSlots() {
      const response = await fetch(
        "http://127.0.0.1:8000/api/slots" + this.selectedEvent_id,
        {
          method: "GET",
          headers: {
            "Content-Type": "application/json",
            Accept: "application/json",
          },
        }
      );
      const data = await response.json();
      this.slots = data.slots;
    },
  },
};
</script>

<style scoped>
h1,
h2,
h3 p {
  color: rgb(86, 82, 82);
  font-weight: bold;
}
.componenterinos {
  inline-size: 100%;
  display: flex;
  text-align: center;
}
</style>
