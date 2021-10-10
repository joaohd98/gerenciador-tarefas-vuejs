<template>
  <div id="main">
    <Home v-if="token" @token="setToken" />
    <Login v-else @token="setToken" />
  </div>
</template>

<script>
import Login from "./components/pages/login";
import Home from "./components/pages/home";

export default {
  data() {
    return {
      token: localStorage.getItem("accessToken"),
    }
  },
  components: {
    Login,
    Home,
  },
  methods: {
    setToken(t) {
      this.token = t;
    }
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">

</style>
