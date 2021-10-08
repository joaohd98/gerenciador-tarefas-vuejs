<template>
  <div class="container-header">
      <img src="../../assets/images/logo.svg" alt="Logo Fiap" class="logo"/>
      <button onClick={showModal}>
        <span>+</span> Adicionar Tarefa
      </button>
      <div class="mobile">
        <span>Olá, {{userName}}</span>
        <img src="../../assets/images/exit-mobile.svg" alt="Deslogar" @click="doLogout()"/>
      </div>
      <div class="desktop">
        <span>Olá, {{userName}}</span>
        <img src="../../assets/images/exit-desktop.svg" alt="Deslogar" @click="doLogout()"/>
      </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      userName: localStorage.getItem("userName").split(' ')[0] || '',
    }
  },
  methods: {
    doLogout()  {
      localStorage.removeItem('accessToken');
      localStorage.removeItem('userName');
      localStorage.removeItem('userEmail');

      this.$emit("doLogout", "");
    },
  },
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
