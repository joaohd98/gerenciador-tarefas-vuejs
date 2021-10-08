<template>
  <div>
    <h1>Home</h1>
    <button type="button" @click="leave()">Sair</button>
  </div>
</template>

<script>
export default {
  methods: {
    leave() {
      localStorage.removeItem('accessToken');
      localStorage.removeItem('userName');
      localStorage.removeItem('userEmail');

      this.$emit("token", "");
    }
  }
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
