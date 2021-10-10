<template>
  <div id="main">
    <Home v-if="currentPage === 'home'" @token="setToken" />
    <Register v-if="currentPage === 'register'" @token="setToken" @goLogin="goLogin" />
    <Login v-if="currentPage === 'login'" @token="setToken" @goRegister="goRegister" />
  </div>
</template>

<script>
import Login from "./components/pages/login";
import Home from "./components/pages/home";
import Register from "./components/pages/register";

export default {
  data() {
    return {
      currentPage: "",
    }
  },
  components: {
    Login,
    Home,
    Register,
  },
  created() {
    const token  = localStorage.getItem("accessToken");

    if(token) {
      this.currentPage = "home";
    } else {
      this.currentPage = "login";
    }
  },
  methods: {
    setToken(t) {
      if(t) {
        this.currentPage = "home";
      }  else {
        this.currentPage = "login";
      }
    },
    goLogin() {
      this.currentPage = "login";
    },
    goRegister() {
      this.currentPage = "register";
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">

</style>
