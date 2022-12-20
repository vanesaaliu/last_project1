<template>
  <div id="app">
    <div class="first-page">
    <router-link to="/"><h3>Home</h3></router-link>
    <router-link to="/movies"><h3>Movies</h3></router-link>
  </div>
    <router-view/>

  </div>
</template>

<style>
#app {
  padding: 30px;
  padding-top:40px
}
.first-page{
   display: flex;
    justify-content: center;
}
 h3{
    padding-right: 15px;
    font-weight: 700;
    font-size: 25px;
    color: #485fc7;
  }
nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
