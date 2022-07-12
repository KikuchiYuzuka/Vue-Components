<template>
  <div id="app">
      <div class="content">
        <nav>
          <router-link to="/">Home</router-link> |
          <router-link to="/SearchForm">SearchForm</router-link> |
          <router-link to="/Table">Table</router-link>
          <router-link to="/CheckPassword">CheckPassword</router-link>


        </nav>
        <router-view/>
      </div>
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

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
