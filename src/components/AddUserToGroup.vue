<template>
  <h1>event_id : {{ event_id }}</h1>
  <div>
    <label for="">Recherche de participant : </label>
    <input
      type="text"
      v-model="searchTerm"
      class=""
      placeholder="Entrez un participant"
    />
    <div class="tableau">
      <table>
        <thead>
          <tr>
            <th>Utilisateurs inscrits</th>
          </tr>
        </thead>
        <tbody>
          <tr>
            <td class="td">Prénom</td>
            <td class="td">Nom</td>
            <td class="td">Email</td>
            <td class="td">Add</td>
          </tr>

          <tr v-for="user in filterByName" :key="user.id">
            <td>{{ user.firstname }}</td>
            <td>{{ user.lastname }}</td>
            <td>{{ user.email }}</td>

            <td><button @click="addToGroup(user.id)">+</button></td>
          </tr>
        </tbody>
      </table>
    </div>
  </div>
</template>

<script>
export default {
  beforeMount() {
    this.getUsers();
  },
  data() {
    return {
      users: [],
      searchTerm: "",
    };
  },

  computed: {
    filterByName() {
      return this.users.filter((user) => {
        return (
          user.firstname
            .toLowerCase()
            .includes(this.searchTerm.toLowerCase()) ||
          user.lastname.toLowerCase().includes(this.searchTerm.toLowerCase())
        );
      });
    },
  },

  methods: {
    /* Recherche de tous les utilisateurs inscrits */
    async getUsers() {
      console.log();
      const response = await fetch("http://127.0.0.1:8000/api/showusers", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      });
      const data = await response.json();
      this.users = data.users;
    },

    async addToGroup(userId) {
      console.log(
        "entrée dans addToGroup avec les valeurs user_id = " +
          userId +
          " et group_id = " +
          this.$route.params.group_id
      );
      const body = {
        user_id: userId,
        group_id: this.$route.params.group_id,
      };

      const response = await fetch("http://127.0.0.1:8000/api/group-users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });
      console.log("sortie addToGroup");

      const data = await response.json();

      this.$emit("UserAdded");

      this.feedbackMessage = data.message;
    },
  },
};
</script>

<style scoped>
table,
.td {
  border: 1px solid #333;
}

thead {
  background-color: #333;
  color: #fff;
}

.tableau {
  display: flex;
  justify-content: center;
  margin-top: 2%;
}
</style>
