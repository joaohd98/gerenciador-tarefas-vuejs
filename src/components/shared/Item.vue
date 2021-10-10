
<template>
  <div class="container-item" :class="getClassActive" @click="onClickCard">
    <img :src="getImageSource" :alt="getImageAlt" />
    <div>
      <p :class="getClassFinished">{{task && task.name}}</p>
      <span>{{getDateText}}</span>
    </div>
    <b-modal v-model="isModalOpen" hide-footer hide-header>
      <ModalEdit
        @doRefresh="doRefresh"
        :id="task._id"
        :name="task.name"
        :finish-prevision-date="task.finishPrevisionDate"
        :finish-date="task.finishDate"
      />
    </b-modal>
  </div>
</template>

<script>
import moment from "moment";
import ModalEdit from "./ModalEdit";

export default {
  data() {
    return {
      isModalOpen: false,
    };
  },
  components: {
    ModalEdit,
  },
  props: {
    task: {
      name: "",
      finishPrevisionDate: "",
      finishDate: "",
    }
  },
  methods: {
    onClickCard() {
      if(!this.task.finishDate) {
        this.isModalOpen = true
      }
    },
    doRefresh() {
      this.isModalOpen = false;
      this.$emit("doRefresh");
    }
  },
  computed: {
    getClassFinished() {
      if(this.task && this.task.finishDate) {
        return "finished";
      }

      return "";
    },
    getClassActive() {
      if(this.task && this.task.finishDate) {
        return "active";
      }

      return "";
    },
    getImageSource() {
      if(this.task && this.task.finishDate){
        return require("../../assets/images/check.svg");
      }

      return require("../../assets/images/uncheck.svg");
    },
    getImageAlt() {
      if(this.task && this.task.finishDate) {
        return "Tarefa concluida";
      }

      return "Tarefa não concluida";
    },
    getDateText(){
      if(this.task && this.task.finishDate){
        return `Concluído em: ${moment(this.task.finishDate,"yyyy-MM-DD").format('DD/MM/yyyy')}`;
      }
      if(this.task && this.task.finishPrevisionDate){
        return `Previsão de conclusão em: ${moment(this.task.finishPrevisionDate, "yyyy-MM-DD").format('DD/MM/yyyy')}`;
      }
      return 'Previsão de conclusão em:';
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
