<template>
<header>
  <nav>
    <router-link to="/">
    <h2>Movies Couch</h2>
    </router-link>
  </nav>
</header>
<router-view/>
</template>

<script>
import env from '@/env.js';

export default ({
  setup() {
    if(!env.apikey) {
    alert("Please add your API Key in environments")
    }
  }
})
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
header {
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 10px 16px;
  background-color: #2C3D4E;
  box-shadow: 0px 0px 6px rgba(0, 0, 0, 0.1);

}
h1 {
  color: #000;
  font-size: 28px;
}
  h3 {
  color: #2c3e50;;
  font-size: 28px;
}
span {
  color: #42B883;
}
nav {
  padding: 30px;
}
nav a {
  font-weight: bold;
  color: #42b983;
}
nav a.router-link-exact-active {
  color: #42b983;
}
</style>
