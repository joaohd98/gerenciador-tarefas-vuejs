<template>
  <div class="container-home">
    <Header @doLogout="logout" @openModal="openModalAdd" />
    <Filters
      :finishPrevisionStart="finishPrevisionStart"
      :finishPrevisionEnd="finishPrevisionEnd"
      :status="status"
      @setFinishPrevisionStart="setFinishPrevisionStart"
      @setFinishPrevisionEnd="setFinishPrevisionEnd"
      @setStatus="setStatus"
    />
    <List :tasks="tasks" @doRefresh="getTasksWithFilters"/>
    <Footer @openModal="openModalAdd" />
    <b-modal v-model="isModalAddOpen" hide-footer hide-header>
      <ModalAdd @doSave="doSave" @closeModal="closeModalAdd" />
    </b-modal>
  </div>
</template>

<script>

import Header from "../shared/Header";
import Footer from "../shared/Footer";
import Filters from "../shared/Filters";
import List from "../shared/List";
import ModalAdd from "../shared/ModalAdd";

export default {
  data() {
    return {
      tasks: [],
      finishPrevisionStart: "",
      finishPrevisionEnd: "",
      status: 0,
      isModalAddOpen: false,
    }
  },
  created(){
    this.getTasksWithFilters();
  },
  components: {Filters, Footer, List, Header, ModalAdd},
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
    },
    openModalAdd() {
      this.isModalAddOpen = true;
    },
    closeModalAdd() {
      this.isModalAddOpen = false;
    },
    doSave() {
      this.isModalAddOpen = false;
      this.getTasksWithFilters();
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
