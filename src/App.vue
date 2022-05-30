<template>
  <div id="app">
    <div class="container">

      <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
        <a style="padding-left:20px" class="navbar-brand" href="#">EMPRESTIMOS</a>
        <div class="collapse navbar-collapse" id="navbarSupportedContent">
          <ul class="navbar-nav mr-auto">
            <li class="nav-item active">
              <router-link class="nav-link" to="/" href="#">Home</router-link>
            </li>
            <li class="nav-item">
              <router-link to="/clientes" class="nav-link" href="#">Clientes</router-link>
            </li>
            
          </ul>
        </div>
      </nav>
      <br>

    </div>
    <router-view/>
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
