<template>
  <div class="container-home">
    <Header @doLogout="logout" />
    <Footer />
  </div>
</template>

<script>

import Header from "../shared/Header";
import Footer from "../shared/Footer";

export default {
  components: {Footer, Header},
  methods: {
    logout() {
      this.$emit("token", "");
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
