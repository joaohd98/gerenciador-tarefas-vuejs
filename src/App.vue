<template>
  <div id="main">
    <home v-if="token" @token="setToken" />
    <login v-else @token="setToken" />
  </div>
</template>

<script>
import login from "./components/pages/login";
import home from "./components/pages/home";

export default {
  data() {
    return {
      token: localStorage.getItem("accessToken"),
    }
  },
  components: {
    login,
    home,
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
