<template>
  <h4>
    Nom: <span>{{ title }}</span>
  </h4>
  <p>
    Date de début: <span>{{ start }}</span>
  </p>
  <p>
    Date de fin: <span>{{ duration }}</span>
  </p>
  <p>
    Lieu: <span>{{ teams }}</span>
  </p>
  <div class="voirsuppr">
    <div>
      <button id="button">Voir</button>
    </div>
    <div>
      <button id="button">Supprimer</button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    title: String,
    start: Date,
    duration: Number,
    teams: Number,
    event_id: Number,
  },
};
</script>
