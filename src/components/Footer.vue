<template>
  <div id="footerContainer">
    <footer class="footer">
      <div class="copyright">© 2022 Copyright: Nice Start(s) Up</div>
      <div id="homeMadeLogo">Hackathon<span id="letter">(s)</span> manager</div>
      <div class="footerMentions">
        <p>A propos de Nice Start(s) Up</p>
        <p>Nous contacter</p>
        <p>Mentions légales</p>
      </div>
    </footer>
  </div>
</template>

<style>
#footerContainer {
  width: 100%;
}
.footer {
  background-color: rgba(0, 0, 0, 0.815);
  bottom: 0;
  color: #969696;
  font-family: revert;
  font-size: 14px;
  font-weight: normal;
  justify-content: space-around;
  flex-direction: row;
  align-content: center;
  align-items: center;
  position: relative;
  display: flex;
}

#homeMadeLogo {
  color: whitesmoke;
  letter-spacing: 1px;
  font-size: x-large;
  margin-top: 20px;
  margin-bottom: 20px;
}

#letter {
  color: red;
}

.copyright {
  margin-left: 10px;
}

.footerMentions {
  display: flex;
  flex-direction: column;
  justify-content: space-around;
  align-items: center;
  margin: 5px 10px 5px 0;
}
</style>
