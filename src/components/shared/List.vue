<template>
  <div class="container-list" :class="getClassEmpty">
    <Item v-if="listHasItems" v-for="task of tasks" :task="task" v-bind:key="task._id" @doRefresh="$emit('doRefresh')" />
    <div class="empty-list" v-if="!listHasItems">
      <img src="../../assets/images/empty-list.svg" alt="Nenhuma tarefa encontrada" />
      <p>Você ainda não possui tarefas cadastradas!</p>
    </div>
  </div>
</template>

<script>

import Item from './Item.vue';

export default {
  props: {
    tasks : []
  },
  computed : {
    listHasItems(){
      return this.tasks && this.tasks.length > 0
    },
    getClassEmpty(){
      if(this.tasks && this.tasks.length > 0){
        return "";
      }
      return "empty";
    }
  },
  components : {
    Item
  }
}
</script>
