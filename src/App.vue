<template>
  <div id="nav">
    <router-link :to="{ name: 'Home' }">Products</router-link> |
    <router-link :to="{ name: 'About' }">About</router-link>
  </div>
  <router-view />
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  background-color: rgb(230, 221, 221);
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
.button {
  margin: 5px;
  font-size: 18px;
  background-color: black;
  color: white;
  border-radius: 7%;
  padding: 10px;
  cursor: pointer;
  border: none;
}
.button:hover {
  background-color: green;
}

.disabledButton,
.disabledButton:hover {
  background-color: #d8d8d8;
  cursor: not-allowed;
}
li {
  font-size: 20px;
  list-style: none;
  text-align: left;
  margin: 5px;
  padding: 5px;
  background-color: powderblue;
}
</style>
