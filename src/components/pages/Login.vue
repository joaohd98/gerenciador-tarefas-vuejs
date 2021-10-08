<template>
  <div class="container-login">
    <img class="logo" src="../../assets/images/logo.svg" alt="logo fiap"/>
    <form>
      <p>{{msgError}}</p>
      <div class="input">
        <img src="../../assets/images/mail.svg" alt="email" />
        <input type="email" placeholder="Email" v-model="body.email">
      </div>
      <div class="input">
        <img src="../../assets/images/lock.svg" alt="password" />
        <input type="password" placeholder="Senha" v-model="body.password"/>
      </div>
      <button type="button" @click="doLogin()">{{labelButton}}</button>
    </form>
  </div>
</template>

<script>
export default {
  data() {
    return {
      msgError: "",
      labelButton: "Login",
      disabledButton: false,
      body: {
        email: "",
        password: "",
      }
    }
  },
  methods: {
    doLogin() {
      if(!this.body.email || !this.body.password) {
        this.msgError = "Favor informar usuario e senha"
        return;
      }

      this.labelButton = "...Carregando";
      this.disabledButton = true;

      this.$http.post("login", this.body)
        .then(response => response.json())
        .then(result => {
          this.labelButton = "Login";
          this.disabledButton = false;

          console.log(result);
        })
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
