<script setup>
  import { reactive } from "vue";
  import Cabecalho from './components/Cabecalho.vue';
  import Formulario from './components/Formulario.vue';
  import ListaDeTarefas from './components/ListaDeTarefas.vue';

  const estadoLista = reactive({
    filtro: 'todas',
    tarefaNova: '',
    tarefas: [
        
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
    <Formulario :trocra-filtro="evento => estadoLista.filtro = evento.target.value" :tarefa-nova="estadoLista.tarefaNova" :edita-tarefa-nova="evento => estadoLista.tarefaNova = evento.target.value" :cadastra-tarefa="cadastrarTarefa"></Formulario>
    <ListaDeTarefas :tarefas="getTarefasFilter()" :tarefas-filtro="getTarefasFilter().length" :tarefas-pendentes="getTarefasPendentes().length"></ListaDeTarefas>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
