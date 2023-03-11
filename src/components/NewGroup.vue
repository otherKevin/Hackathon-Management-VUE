<template>
  <section>
    <div>
      <button @click="submit">Inscrire</button>
      <div>
        <CreateGroup></CreateGroup>
      </div>
    </div>
  </section>
</template>

<script>
import CreateGroup from "./CreateGroup.vue";

export default {
  components: {
    // Generique,
    CreateGroup,
  },
  data() {
    return {
      formulaireData: [],
    };
  },
  methods: {
    async submit() {
      let retourRequete = await fetch();
      let donnees = await retourRequete.json();
      this.formulaireData = donnees.list;
    },
  },
};
</script>

<style scoped></style>
