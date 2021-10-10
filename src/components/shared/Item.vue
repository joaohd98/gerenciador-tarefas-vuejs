
<template>
  <div class="container-item" :class="getClassActive">
    <img :src="getImageSource" :alt="getImageAlt" />
    <div>
      <p :class="getClassFinished">{{task && task.name}}</p>
      <span>{{getDateText}}</span>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: {
    task: {
      name: "",
      finishPrevisionDate: "",
      finishDate: "",
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
        return `Concluído em: ${moment(this.task.finishDate).format('DD/MM/yyyy')}`;
      }
      if(this.task && this.task.finishPrevisionDate){
        return `Previsão de conclusão em: ${moment(this.task.finishPrevisionDate).format('DD/MM/yyyy')}`;
      }
      return 'Previsão de conclusão em:';
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
