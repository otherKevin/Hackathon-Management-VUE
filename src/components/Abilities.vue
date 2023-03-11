<template>
  <hr />
  <section id="container">
    <div>
      <h1>Mes compétences</h1>
      <br />

      <form>
        <div class="container">
          <div class="row g-2">
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>Développeur</p>
                <input type="checkbox" name="dev" v-model="dev" />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>UI/UX</p>
                <input type="checkbox" name="design" v-model="design" />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>Maker</p>
                <input type="checkbox" name="maker" v-model="maker" />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>Management</p>
                <input type="checkbox" name="management" v-model="management" />
              </div>
            </div>
          </div>
        </div>
        <button type="submit" value="Valider" id="button">Valider</button>
        <div class="container">
          <div class="row g-2">
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>Commercial</p>
                <input type="checkbox" name="commercial" v-model="commercial" />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>OPS</p>
                <input type="checkbox" name="ops" v-model="ops" />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>Communication</p>
                <input
                  type="checkbox"
                  name="communication"
                  v-model="communication"
                />
              </div>
            </div>
            <div class="abilities col-6">
              <div class="p-3 bg-light">
                <p>design graphique</p>
                <input
                  type="checkbox"
                  name="desiGraph"
                  v-model="designGraphique"
                />
              </div>
            </div>
          </div>
        </div>
      </form>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      users: [],
      dev: "",
      design: "",
      maker: "",
      management: "",
      commercial: "",
      communication: "",
      ops: "",
      designGraph: "",
    };
  },

  methods: {
    /* Récupération */
    async getAbilities() {
      const response = await fetch("http://127.0.0.1:8000/api/users", {
        method: "GET",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
      });
      const data = await response.json();
      this.abilities = data.abilities;
    },

    /* Création des modifs */
    async createAbilities() {
      const body = {
        dev: this.dev,
        design: this.design,
        maker: this.maker,
        management: this.management,
        commercial: this.commercial,
        communication: this.communication,
        ops: this.ops,
        designGraph: this.designGraph,
      };

      const response = await fetch("http://127.0.0.1:8000/api/users", {
        method: "POST",
        headers: {
          "Content-Type": "application/json",
          Accept: "application/json",
        },
        body: JSON.stringify(body),
      });

      const data = await response.json();

      this.feedbackMessage = data.message;

      this.getAbilities();
    },
  },

  mounted() {
    this.getAbilities();
  },
};
</script>

<style scoped>
.container {
  margin-top: 0.5em;
  margin-bottom: 0.5em;
}

h1 {
  font-size: 2em;
}

h1,
p,
label {
  color: rgb(86, 82, 82);
}

p {
  padding: 5px;
  margin-left: 20px;
}

#container {
  height: 100%;
}

input {
  margin-left: 10px;
  top: -7px;
  position: relative;
}

#formStyle {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  margin: 40px;
}

#button {
  border: 2px solid GREY;
  background-color: white;
  color: grey;
  height: 60px;
  width: 180px;
  cursor: pointer;
  padding: 10px;
  font-size: 20px;
  display: inline-flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin-top: 100px;
  margin-bottom: 100px;
}

#button:hover {
  border: 2px solid rgb(219, 117, 117);
  background-color: rgb(219, 117, 117);
  color: white;
  font-weight: bold;
}

.abilities {
  border: 2px solid red;
}
</style>
