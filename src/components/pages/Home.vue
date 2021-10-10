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
import List from "../shared/List";

export default {
  data() {
    return {
      finishPrevisionStart: "",
      finishPrevisionEnd: "",
      status: 0,
    }
  },
  created(){
    this.getTasksWithFilters();
  },
  components: {Filters, Footer, List, Header},
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
    getTasksWithFilters(){
      let filters = '?status='+this.status;

      if(this.finishPrevisionStart){
        filters += '&finishPrevisionStart='+this.finishPrevisionStart
      }

      if(this.finishPrevisionEnd){
        filters += '&finishPrevisionEnd='+this.finishPrevisionEnd
      }

      const token = localStorage.getItem('accessToken')

      this.$http.get('task' + filters, {headers : {'Authorization' : 'Bearer ' + token}})
        .then(r => r.json())
        .then(result => {
          this.tasks = result;
        });
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
