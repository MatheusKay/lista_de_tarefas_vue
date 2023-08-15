<script setup>
  import { reactive } from "vue";
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estadoLista = reactive({
    filtro: 'todas',
    tarefaNova: '',
    tarefas: [
      {
        titulo:'Estudar',
        finalizado: false,
      },  
    ]
  })

  function getTarefasPendentes() {
    return estadoLista.tarefas.filter(tarefa => !tarefa.finalizado)
  }

  function getTarefasFinalizadas() {
    return estadoLista.tarefas.filter(tarefa => tarefa.finalizado)
  }

  function getTarefasFilter() {
    const {filtro} = estadoLista;

    switch (filtro) {
      case 'pendentes':
        return getTarefasPendentes();
      case 'finalizadas': 
        return getTarefasFinalizadas();
      default:
        return estadoLista.tarefas
    }
  }

  const cadastrarTarefa = () => {
    const tarefaNova = {
      titulo: estadoLista.tarefaNova,
      finalizado: false,
    }
    estadoLista.tarefas.push(tarefaNova)
    estadoLista.tarefaNova = '';
  }
</script>

<template>
  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length"></Cabecalho>
    <Formulario :tarefa-nova="estadoLista.tarefaNova" :edita-tarefa-nova="evento => estadoLista.tare = evento.target.value" :cadastra-tarefa="cadastrarTarefa"></Formulario>
    <!-- <ListaDeTarefas :get-tarefas-filtro="getTarefasFilter()" :tarefa-finalizada="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :titulo-tarefa="tarefa.titulo" /> -->
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
