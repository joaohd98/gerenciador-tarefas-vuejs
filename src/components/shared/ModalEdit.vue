<template>
  <div class="container-modal">
    <p v-if="msgError" class="error">{{msgError}}</p>
    <div class="modal-body">
      <p>Adicionar Tarefa</p>
      <input type="text" placeholder="Criar uma tarefa" v-model="body.name" />
      <input type="date" placeholder="Data de previsão" v-model="body.finishPrevisionDate" />
      <input type="date" placeholder="Data de conclusão" v-model="body.finishDate" />
    </div>
    <div class="modal-footer">
      <div class="button col-12">
        <button @click="doSave">{{labelButton}}</button>
        <span @click="doDelete">Excluir Tarefa</span>
      </div>
    </div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  data() {
    return {
      body: {
        name: this.name,
        finishPrevisionDate: moment(this.finishPrevisionDate, "yyyy-MM-DD").format("yyyy-MM-DD"),
        finishDate: this.finishDate ? moment(this.finishDate, "yyyy-MM-DD").format("yyyy-MM-DD") : "",
      },
      isLoading: false,
      msgError: "",
      labelButton: "Salvar alterações",
    }
  },
  props: {
    id: "",
    name: "",
    finishPrevisionDate: "",
    finishDate: "",
  },
  methods: {
    executeRequestUpdate(name, finishPrevisionDate, finishDate) {
      const token = localStorage.getItem('accessToken')

      return this.$http.put(
        'task?id=' + this.id,
        {name, finishPrevisionDate, finishDate},
        {headers : {'Authorization' : 'Bearer ' + token}}
      ).then(r => r.json());
    },
    executeRequestDelete() {
      const token = localStorage.getItem('accessToken')

      return this.$http.delete(
        'task?id=' + this.id,
        {headers : {'Authorization' : 'Bearer ' + token}}
      ).then(r => r.json());
    },
    doSave() {
      this.msgError = "";
      this.isLoading = true;
      this.labelButton = "Carregando...";

      const {id} = this;
      const {name, finishPrevisionDate, finishDate} = this.body;

      if (!id || !name || !finishPrevisionDate) {
        this.msgError = 'Favor preencher os dados';
        this.isLoading = false;
        this.labelButton = "Salvar alterações";
        return;
      }

      this.executeRequestUpdate(name, finishPrevisionDate, finishDate).then(result => {
        if (!result || !result.msg) {
          this.msgError = 'Nao foi possivel salvar a tarefa!';
          this.isLoading = false;
          this.labelButton = "Salvar alterações";
          return
        }

        this.$emit("doRefresh");
      }).catch(e => {
        this.isLoading = false;
        this.labelButton = "Salvar alterações";

        if (e.error) {
          this.msgError = e.response.data.error;
        } else {
          this.msgError = 'Ocorreu erro ao adicionar tarefa tente novamente!';
        }
      });
    },
    doDelete() {
      this.msgError = "";
      this.isLoading = true;
      this.labelButton = "Carregando...";

      this.executeRequestDelete().then(() => {
        this.$emit("doRefresh", "");
      }).catch(() => {
        this.msgError = 'Nao foi possivel deleter a tarefa!';
        this.isLoading = false;
        this.labelButton = "Salvar alterações";
      });
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
