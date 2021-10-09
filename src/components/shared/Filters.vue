<template>
  <div class="container-filters">
    <div class="title">
      <span>Tarefas</span>
      <img src="../../assets/images/filtro.svg" alt="filtrar tarefas" @click="showFilters = !showFilters" />
      <div class="form">
        <div>
          <label>Data prevista de conclusão de: </label>
          <input type="date" :value="finishPrevisionStart" @input="$emit('setFinishPrevisionStart', $event.target.value)"/>
        </div>
        <div>
          <label>Até: </label>
          <input type="date" :value="finishPrevisionEnd" @input="$emit('setFinishPrevisionEnd', $event.target.value)" />
        </div>
        <div class="line" />
        <div>
          <label>Status: </label>
          <select :value="status" @input="$emit('setStatus', $event.target.value)">
            <option value=0>Todas</option>
            <option value=1>Ativas</option>
            <option value=2>Concluidas</option>
          </select>
        </div>
      </div>
    </div>
    <div class="filters-mobile" v-if="showFilters">
      <div>
        <label>Periodo de: </label>
        <input type="date" :value="finishPrevisionStart" @input="$emit('setFinishPrevisionStart', $event.target.value)"/>
      </div>
      <div>
        <label>Periodo até: </label>
        <input type="date" :value="finishPrevisionEnd" @input="$emit('setFinishPrevisionEnd', $event.target.value)" />
      </div>
      <div>
        <label>Status: </label>
        <select :value="status" @input="$emit('setStatus', $event.target.value)">
          <option value=0>Todas</option>
          <option value=1>Ativas</option>
          <option value=2>Concluidas</option>
        </select>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      showFilters: false,
    }
  },
  props: {
    finishPrevisionStart: "",
    finishPrevisionEnd: "",
    status: 0,
  }
}
</script>

<style lang="scss" rel="stylesheet/scss">

</style>
