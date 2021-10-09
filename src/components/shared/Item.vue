
<template>
  <div class="container-item" :class="getClassFinished">
    <img :src="require('../../assets/images/' + getImageSource)" :alt="getImageAlt" />
    <div>
      <p :class={getClassActive}>{task.name}</p>
      <span>{getDate(task.finishDate, task.finishPrevisionDate)}</span>
    </div>
  </div>
</template>

<script>
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
        return "concluido";
      }

      return "";
    },
    getClassActive() {
      if(this.task && this.task.finishDate) {
        return "ativo";
      }

      return "";
    },
    getImageSource() {
      if(this.task && this.task.finishDate) {
        return "check.svg";
      }

      return "uncheck.svg";
    },
    getImageAlt() {
      if(this.task && this.task.finishDate) {
        return "Tarefa concluida";
      }

      return "Tarefa não concluida";
    },
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
