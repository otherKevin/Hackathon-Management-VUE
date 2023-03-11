<template>
  <div>
    <h1>Création de votre compte</h1>
    <form @submit.prevent="createUser">
      <div>
        <label for="firstname">Prénom : </label>
        <input
          type="text"
          name="firstname"
          id="firstname"
          placeholder="Prénom"
          v-model="firstname"
        />
      </div>
      <br />
      <div>
        <label for="lastname">Nom : </label>
        <input
          type="text"
          name="lasttname"
          id="lastname"
          placeholder="Nom"
          v-model="lastname"
        />
      </div>
      <br />
      <div>
        <label for="email">Email : </label>
        <input
          type="email"
          name="email"
          id="email"
          placeholder="Email"
          v-model="email"
        />
      </div>
      <br />
      <div>
        <label for="password">Mot de passe : </label>
        <input
          type="password"
          name="password"
          id="password"
          placeholder="password"
          v-model="password"
        />
      </div>
      <br />
      <input id="validate" type="submit" value="Valider" />
    </form>
    <!-- <p>event_id : {{ this.$route.params.event_id }}</p> -->

    <p v-if="status == true">
      Création de compte réussie
      <br />
    </p>
    <p v-else-if="status == false">Création de compte échouée</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      status: null,
      message: "",
      firstname: "",
      lastname: "",
      email: "",
      password: "",
      message: "",
    };
  },
  methods: {
    /* Création d'un user */

    async createUser() {
      const body = {
        firstname: this.firstname,
        lastname: this.lastname,
        email: this.email,
        password: this.password,
        event_id: this.$route.params.event_id,
      };

      const response = await fetch("http://127.0.0.1:8000/api/auth/register", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });
      const data = await response.json();
      this.message = data.message;
      this.status = data.status;

      if (data.status === true) {
        localStorage.setItem("savedUserToken", data.token);

        //REDIRECTION VERS LA PAGE DE L'EVENEMENT APRES INSCRIPTION
        window.location.href = "/#/eventunique/" + this.$route.params.event_id;
      }
    },
  },
};
</script>

<style scoped>
#validate {
  margin-bottom: 13%;
}
</style>
