<template>
  <hr />
  <div>
    <h1>Espace déconnexion</h1>
    <br />
    <div id="formStyle">
      <button @click="disconnect">Se déconnecter</button>
    </div>
  </div>
  <QRgenerator></QRgenerator>
</template>

<script>
export default {
  methods: {
    disconnect() {
      localStorage.removeItem("savedUserToken");
      window.location.reload();
    },
  },
};
</script>

<style scoped>
h1 {
  color: rgb(86, 82, 82);
}

#formStyle {
  display: flex;
  flex-direction: column;
  flex-wrap: nowrap;
  align-content: center;
  justify-content: center;
  align-items: center;
}

button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  height: 60px;
  width: 180px;
  cursor: pointer;
  padding: 10px;
  font-size: 20px;
  position: fixed;
  top: 600px;
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}
</style>
