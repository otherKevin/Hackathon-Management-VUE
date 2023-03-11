<template>
  <!-- APPEL DU COMPOSANT EventUnique avec en props les valeurs de l'événement séléctionné grâce à l'id passé en paramètre d'URL -->
  <div class="eventDisplay">
    <EventUnique
      v-if="event.id != null"
      :name="event.name"
      :start="event.start"
      :end="event.end"
      :location="event.location"
      :event_id="event.id"
      :viewing="true"
    />
    <!-- CAS D'UN UTILISATEUR NON CONNECTE -->
    <router-link
      v-if="token == null"
      :to="{
        name: 'creation de compte',
        params: {
          event_id: $route.params.event_id,
        },
      }"
    >
      <br />
      <button class="">S'inscrire</button></router-link
    >
    <!-- CAS D'UN UTILISATEUR CONNECTE -->

    <button v-if="token != null" @click="addUserToEvent">M'inscrire !</button>
  </div>
  <hr />

  <!-- ESPACE ADMIN  -->
  <!-- <div>
    <ModifyEvents :event_id="event.id" @eventModified="getEventUnique" />
  </div> -->

  <!-- ESPACE STAFF -->
  <!-- APPEL DU COMPOSANT CreateGroup AFIN D'AFFICHER LE FORMULAIRE DE CREATION DE GROUPE -->
  <!-- <div class="groupFormDisplay">
    <CreateGroup :event_id="event.id" @groupCreated="getGroupUnique" />
  </div> -->

  <!-- APPEL DU COMPOSANT GroupUnique AVEC UN v-for AFIN D'AFFICHER LA LISTE DES GROUPES LIES A CET EVENEMENT -->
  <div class="allGroupsIn@/components/EventUnique.vue">
    <h2>Listes des groupes actuellement enregistrés dans cet événement :</h2>
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
  </div>
  <div>
    <QrGenerator />
  </div>
</template>

<script>
import EventUnique from "@/components/EventUnique.vue";
import CreateGroup from "@/components/CreateGroup.vue";
import GroupUnique from "@/components/GroupUnique.vue";
import ModifyEvents from "@/components/ModifyEvents.vue";

import CreateUser from "@/components/CreateUser.vue";

export default {
  beforeMount() {
    this.getEventUnique();
    this.getGroupUnique();
  },

  data() {
    return {
      event: {},
      groups: [],
      token: localStorage.getItem("savedUserToken"),
      /* event_id: this.event.id, */ // UTILISATION POUR LE PROVIDE
    };
  },
  /*   provide() {
    return {
      event_id: computed(() => this.event_id),
    };
  }, */

  components: {
    EventUnique,
    CreateGroup,
    GroupUnique,
    ModifyEvents,
    CreateUser,
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

    /* Récupération de tous les groups uniques, liés à l'événement dans lequel on se trouve */
    async getGroupUnique() {
      const response = await fetch(
        "http://127.0.0.1:8000/api/events/" +
          this.$route.params.event_id +
          "/groups",
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
    },

    async addUserToEvent() {
      alert("entrée dans addUserToEvent");
      const body = {
        event_id: this.$route.params.event_id,
      };

      const response = await fetch("http://127.0.0.1:8000/api/event-users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          Authorization: `Bearer ${localStorage.getItem("savedUserToken")}`,
        },
        body: JSON.stringify(body),
      });
      const data = await response.json();

      this.feedbackMessage = data.message;
    },
  },
};
</script>

<style scoped>
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
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}
</style>
