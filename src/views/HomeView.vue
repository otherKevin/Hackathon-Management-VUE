<template>
  <section id="bodyImage">
    <h2>Prochain évènement</h2>
    <h2>H - 1 min</h2>
  </section>
  <div class="event">
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
  name: "App",

  data() {
    return {
      events: [],
      token: localStorage.getItem("savedUserToken"),
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
/* BODY */
#bodyImage {
  opacity: 0.9;
  background-image: url("../assets/nice.jpeg");
  background-size: cover;
  height: 850px;
  color: white;
  z-index: 200;
  font-size: 70px;
  text-shadow: 2px 2px 2px black;
}

h2 {
  margin: 40px;
  opacity: 1;
  font-size: 1em;
}

.event {
  display: flex;
  justify-content: center;
}
</style>
