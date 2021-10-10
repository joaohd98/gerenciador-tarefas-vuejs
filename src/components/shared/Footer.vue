
<template>
  <div class="container-footer">
    <button @click="openModal">
      <img src="../../assets/images/add.svg" alt="adicionar" /> Adicionar uma Tarefa
    </button>
    <span>© Copyright {{fullYear}}. Todos os direitos reservados.</span>
  </div>
</template>

<script>
export default {
  methods: {
    openModal() {
      this.$emit("openModal", "");
    },
  },
  computed: {
    fullYear() {
      return new Date().getFullYear()
    }
  },
}

</script>

<style lang="scss" rel="stylesheet/scss">

</style>
