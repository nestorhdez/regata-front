<template>

  <div id="app">
    <div id="nav">
      <router-link to="/"><img id="logo" src="./assets/fcv-logo.png" alt="Logotipo"></router-link>
      <div id="links-container">
        <router-link to="/">Regatistas</router-link>
        <router-link to="/contact">Contacto</router-link>
      </div>
    </div>
    <router-view/>
  </div>

</template>

<style>

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  min-height: 100vh;
  background-color: #3b506b;
}

#nav {
  position: fixed;
  width: 100%;
  padding: 8px 30px;
  background-color: #3b506b;
  box-shadow: 0px 0px 3px 0px rgba(0, 0, 0, 0.58);
  display: flex;
  justify-content: space-between;
  align-items: center;
}

#logo {
  width: 45px;
  height: 45px;
}

#nav a {
  text-decoration: none;
}

#links-container a {
  font-weight: bold;
  color: rgba(255, 255, 255, .6);
  margin-left: 15px;
}

#nav a.router-link-exact-active {
  color: rgba(255, 255, 255, 1);
}

</style>
