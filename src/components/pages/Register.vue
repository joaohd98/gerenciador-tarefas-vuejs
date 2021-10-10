<template>
  <div class="container-register">
    <div>
      <div class="back-container">
        <button @click="$emit('goLogin')">Voltar</button>
      </div>
      <div class="form-container">
        <img class="logo" src="../../assets/images/logo.svg" alt="logo fiap"/>
        <form>
          <p>{{msgError}}</p>
          <div class="input">
            <input type="text" placeholder="Name" v-model="body.name">
          </div>
          <div class="input">
            <input type="email" placeholder="Email" v-model="body.email">
          </div>
          <div class="input">
            <input type="password" placeholder="Senha" v-model="body.password"/>
          </div>
          <button type="button" @click="doLogin()">{{labelButton}}</button>
        </form>
      </div>
   </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msgError: "",
      labelButton: "Cadastrar",
      disabledButton: false,
      body: {
        name: "",
        email: "",
        password: "",
      }
    }
  },
  methods: {
    doLogin() {
      if(!this.body.email || !this.body.password ||!this.body.name) {
        this.msgError = "Favor informar todos os dados"
        return;
      }

      this.labelButton = "...Carregando";
      this.disabledButton = true;

      this.$http.post("user", this.body)
        .then(response => response.json())
        .then(result => {
          this.labelButton = "Cadastrar";
          this.disabledButton = false;

          localStorage.setItem('accessToken', result.token);
          localStorage.setItem('userName', this.body.name);
          localStorage.setItem('userEmail', this.body.email);

          this.$emit("token", result.token);

        }).catch(e => {
          console.log(e);

          this.labelButton = "Cadastrar";
          this.disabledButton = false;

          if(e && e.body && e.body.error){
            this.msgError = e.body.error;
          } else {
            this.msgError = "Não foi possivel cadastrar, tente novamente"
          }
        });
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
