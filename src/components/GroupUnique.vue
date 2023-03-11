<template>
  <div class="groupDiv">
    <h2>Nom du Groupe : {{ name }}</h2>
    <p>Sujet : {{ subject }}</p>
    <p>Salle : {{ room }}</p>
    <p>Nombre de membres : {{ members }}</p>
    <p>
      Compétences :
      {{ abilities }}
    </p>

    <router-link
      v-if="!viewing"
      :to="{
        name: 'GroupUniqueShow',
        params: {
          group_id: this.group_id,
        },
      }"
      ><button>Voir le groupe</button>
    </router-link>
    <button>Supprimer</button>
  </div>
</template>

<script>
export default {
  props: {
    name: String,
    subject: String,
    room: String,
    members: Number,
    abilities: String,
    group_id: Number,
    event_id: Number,
    viewing: Boolean,
  },
};
</script>

<style scoped>
button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  padding-left: 20px;
  padding-right: 20px;
  cursor: pointer;
  padding: 10px;
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}
</style>
