<template>
  <div class="container-modal">
    <p v-if="msgError" class="error">{{msgError}}</p>
    <div class="modal-body">
      <p>Adicionar Tarefa</p>
      <input type="text" placeholder="Criar uma tarefa" v-model="name" />
      <input type="date" placeholder="Data de previsão" v-model="finishPrevisionDate" />
    </div>
    <div class="modal-footer">
      <div class="button col-12">
        <button @click="doSave">{{labelButton}}</button>
        <span @click="closeModal">Cancelar</span>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      finishPrevisionDate: "",
      isLoading: false,
      msgError: "",
      labelButton: "Salvar",
    }
  },
  methods: {
    closeModal() {
      this.$emit("closeModal");
    },
    executeRequest(name, finishPrevisionDate) {
      const token = localStorage.getItem('accessToken')

      return this.$http.post(
        'task',
        {name, finishPrevisionDate},
        {headers : {'Authorization' : 'Bearer ' + token}}
      ).then(r => r.json());
    },
    doSave() {
      this.msgError = "";
      this.isLoading = true;
      this.labelButton = "Carregando...";

      try {
        const {name, finishPrevisionDate} = this;

        if (!name || !finishPrevisionDate) {
          this.msgError = 'Favor preencher o nome e data de previsão';
          this.isLoading = false;
          this.labelButton = "Login";
          return;
        }

        this.executeRequest(name, finishPrevisionDate).then(result => {
          if (!result || !result.msg) {
            this.msgError = 'Nao foi possivel salvar a tarefa!';
            this.isLoading = false;
            this.labelButton = "Login";
            return
          }

          this.$emit("doSave", "");
        }).catch(() => {
          throw Error();
        });

      } catch (e) {
        this.isLoading = false;
        this.labelButton = "Login";

        if (e.response.data.error) {
          this.msgError = e.response.data.error;
        } else {
          this.msgError = 'Ocorreu erro ao adicionar tarefa tente novamente!';
        }
      }
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
