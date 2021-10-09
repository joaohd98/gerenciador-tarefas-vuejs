<template>
  <div class="container-home">
    <Header @doLogout="logout" />
    <Filters
      :finishPrevisionStart="finishPrevisionStart"
      :finishPrevisionEnd="finishPrevisionEnd"
      :status="status"
      @setFinishPrevisionStart="setFinishPrevisionStart"
      @setFinishPrevisionEnd="setFinishPrevisionEnd"
      @setStatus="setStatus"
    />
    <Footer />
  </div>
</template>

<script>

import Header from "../shared/Header";
import Footer from "../shared/Footer";
import Filters from "../shared/Filters";

export default {
  data() {
    return {
      finishPrevisionStart: "",
      finishPrevisionEnd: "",
      status: 0,
    }
  },
  components: {Filters, Footer, Header},
  methods: {
    logout() {
      this.$emit("token", "");
    },
    setFinishPrevisionStart(d) {
      this.finishPrevisionStart = d;
    },
    setFinishPrevisionEnd(d) {
      this.finishPrevisionEnd = d;
    },
    setStatus(s) {
      this.status = s;
    },
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
