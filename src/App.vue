<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <Login v-if="!loggedIn" class="login"></Login>
    <Cars v-else></Cars>
  </div>
</template>

<script>
import Cars from "./components/Cars";
import Login from "./components/Login";

export default {
  name: 'app',
  components: {
    Login,
    Cars
  },
  data() {
    return{
      loggedIn: false,
      form: {
        email: '',
        pass: '',
      }
    }
  },
  mounted() {
    if (localStorage.getItem('user')) {
      try {
        this.form = JSON.parse(localStorage.getItem('user'));
        this.loggedIn = true;
      } catch(e) {
        localStorage.removeItem('user');
      }
    }
  },
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.login {
  margin-bottom: 15px;
}  
  
</style>
