<template>
  <hr />
  <div id="mainContainer">
    <h1>Mon profil</h1>

    <!-- FUTUR IMAGE DE PROFIL -->
    <!-- <span>{{ picture }}</span> -->

    <div id="blocContainer">
      <div id="leftContainer" class="container">
        <div>
          <p>Biographie:</p>
          <p class="info">{{ user.bio }}</p>
        </div>
      </div>
      <div id="centerContainer" class="container">
        <p>
          Prénom: <span class="info">{{ user.firstname }}</span>
        </p>
        <p>
          Nom: <span class="info">{{ user.lastname }}</span>
        </p>
        <p>
          Email: <span class="info">{{ user.email }}</span>
        </p>
        <p>
          Mot de passe: <span class="info">{{ user.password }}</span>
        </p>
      </div>
      <div id="rightContainer" class="container">
        <p>
          LinkedIn: <span class="info">{{ user.linkedIn }}</span>
        </p>
        <p>
          GitHub: <span class="info">{{ user.github }}</span>
        </p>
        <p>
          Website: <span class="info">{{ user.website }}</span>
        </p>
        <p>
          PortFolio: <span class="info">{{ user.portfolio }}</span>
        </p>
      </div>
    </div>
    <div id="btnBloc">
      <div>
        <button @click="redirectionBadge">Badge</button>
      </div>
      <div>
        <button @click="$router.push('/modifications')">Modifier</button>
      </div>
      <div>
        <button class="" @click="disconnect">Se déconnecter</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  mounted() {
    this.getUserById();
    this.saveUrl();
  },
  data() {
    return {
      user: [],
    };
  },
  props: {
    token: String,
  },
  // Récupérer les infos d'un USER
  methods: {
    async getUserById() {
      const response = await fetch("http://127.0.0.1:8000/api/my-profile/", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
          Authorization: `Bearer ${localStorage.getItem("savedUserToken")}`,
        },
      });
      const data = await response.json();
      this.user = data.user;
    },

    disconnect() {
      localStorage.removeItem("savedUserToken");
      window.location.href = "/#/home";
    },
    redirectionBadge() {
      window.location.href = "/#/pageqrcode";
    },
    saveUrl() {
      console.log(window.location);
      localStorage.setItem("@currentUrl", window.location.href);
    },
  },
};
</script>
<style scoped>
h1,
p {
  color: rgb(86, 82, 82);
  font-weight: bold;
}

label {
  margin: 10px;
}

#mainContainer {
  max-width: 1280px;
  min-height: 100%;
  margin: 0 auto;
  position: relative;
}
.info {
  color: rgb(219, 117, 117);
}

#blocContainer {
  display: flex;
  flex-direction: row;
  justify-content: center;
  text-align: left;
  margin: 40px;
}

#leftContainer {
  margin-left: 240px;
}

#rightContainer {
  margin-right: 240px;
}

.container {
  width: 20%;
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
  margin-bottom: 5%;
  font-weight: bold;
}

button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}

#btnBloc {
  display: flex;
  justify-content: center;
  position: relative;
  margin: 8%;
}
</style>
