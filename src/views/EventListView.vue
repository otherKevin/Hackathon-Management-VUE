<template>
  <hr />
  <div id="container">
    <h1>Liste des évènements</h1>
    <div>
      <form>
        <EventUnique
          v-for="event in events"
          :key="event.id"
          :name="event.name"
          :start="event.start"
          :end="event.end"
          :location="event.location"
          :event_id="event.id"
          @eventDeleted="getEvents"
        />
      </form>
    </div>
  </div>
</template>

<script>
import CreateEvents from "@/components/CreateEvents.vue";
import EventUnique from "@/components/EventUnique.vue";

export default {
  components: {
    CreateEvents,
    EventUnique,
  },
  data() {
    return {
      events: [],
    };
  },
  mounted() {
    this.getEvents();
  },
  methods: {
    /* Récupération des events */
    async getEvents() {
      const response = await fetch("http://127.0.0.1:8000/api/events", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          Authorization: `Bearer ${localStorage.getItem("savedUserToken")}`,
        },
      });
      const data = await response.json();
      this.events = data.events;
    },
  },
};
</script>

<style scoped>
h1 {
  color: rgb(86, 82, 82);
}

#container {
  height: 100%;
}
</style>
