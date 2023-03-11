<template>
  <div>
    <TestHome
      v-for="event in events"
      :key="event.id"
      :name="event.name"
      :start="event.start"
      :end="event.end"
      :location="event.location"
      :event_id="event.id"
    />
  </div>
</template>

<script>
import TestHome from "@/components/TestHome.vue";

export default {
  components: {
    TestHome,
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

<style scoped></style>
