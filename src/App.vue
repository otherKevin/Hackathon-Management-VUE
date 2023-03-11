<template>
  <body>
    <div id="container">
      <div id="main">
        <header>
          <div id="logoBloc">
            <a href="https://lebocal.academy/"
              ><img src="./assets/logo_bocal.png" alt="" class="logo"
            /></a>
            <h1>HACKATHON<span>(s)</span> MANAGER</h1>
            <a href="https://www.nicestartsup.com/"
              ><img src="./assets/logo_nicestartup.png" alt="" class="logo"
            /></a>
          </div>
        </header>

        <section class="stickyNav">
          <nav>
            <router-link to="/home" class="links">Accueil</router-link>
            <router-link to="/login" class="links">Connexion</router-link>
            <router-link to="/mon-profil" class="links">Mon profil</router-link>
            <router-link to="/eventlist">Evènements</router-link>
            <router-link to="/admin" class="links">Espace admin</router-link>
            <router-link to="/event-management" class="links"
              >Espace staff</router-link
            >
            <router-link to="/abilities" class="links"
              >Mes compétences</router-link
            >
            <router-link to="/qrgenerator" class="links">Qr Code</router-link>
            <router-link to="/pageqrcode" class="links"
              >Page avec QR Code</router-link
            >
          </nav>
        </section>
        <router-view />
      </div>

      <div class="footer">
        <Footer />
      </div>
    </div>
  </body>
</template>

<script>
import "bootstrap/dist/css/bootstrap.min.css";
import HomeView from "./views/HomeView.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "App",
  components: { HomeView, Footer },

  data() {
    return {
      token: localStorage.getItem("savedUserToken"),
    };
  },
};
</script>

<style lang="scss">
//NAV
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}

#routerViewStyle {
  margin-top: 20px;
}

// Déplacer le style à partir d'ici pour le mettre dans des components.
body {
  height: 100%;
  position: relative;
}

header {
  h1 {
    font-size: 60px;
    font-weight: bold;
    color: rgb(86, 82, 82);
    margin: 20px;
  }
}

span {
  color: #e4111e;
}

.stickyNav {
  position: -webkit-sticky;
  position: sticky;
  background-color: rgb(86, 82, 82);
  float: left;
  top: 0px;
  width: 100%;
  z-index: 1;
  height: 60px;
}

a {
  text-decoration-line: none;
  color: white;
  padding: 15px;
  font-size: 14px;
  font-weight: bold;
  text-align: center;
  height: 60px;
  display: inline-flex;
  align-content: center;
  justify-content: center;
  align-items: center;
}

a:hover {
  text-decoration-line: none;
  color: white;
  background-color: white;
  color: rgb(219, 117, 117);
  font-size: 16px;
}

#logoBloc {
  display: flex;
  justify-content: space-around;
  align-items: center;
}

.logo {
  height: 60px;
  min-width: 40px;
  min-width: 100px;
}
#homeMadeLogo {
  color: whitesmoke;
  font-family: fantasy;
  letter-spacing: 1px;
  font-size: x-large;
}

#letter {
  color: red;
}

.links {
  text-decoration-line: none;
}

nav {
  margin-bottom: 20px;
}
#navBar {
  background-color: whitesmoke;
  padding: 4%;
}

#navLink {
  text-decoration: none;
}

.hackTitle {
  display: flex;
}

.hackTitle span {
  color: #e4111e;
  font-size: 50px;
}

.hackTitle h1 {
  display: flex;
  color: black;
}
</style>
