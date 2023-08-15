<script setup>
  import { reactive } from "vue";

  const estadoLista = reactive({
    filtro: 'todas',
    tarefaNova: '',
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizado: false
      },
      {
        titulo: 'Estudar Sass',
        finalizado: false
      },
      {
        titulo: 'Estudar Js',
        finalizado: true
      }
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
    <header class="p-5 md-4 mt-4 bg-light rounded-3">
      <h1>Minhas tarefas</h1>
      <p>
        Voce possui {{ getTarefasPendentes().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="cadastrarTarefa" class="mt-4">
      <div class="row">
        <div class="col">
          <input :value ="estadoLista.tarefaNova" @change="evento => estadoLista.tarefaNova = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estadoLista.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Tarefas pendentes</option>
            <option value="finalizadas">Tarefas finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4" v-for="tarefa in getTarefasFilter()">
      <li class="list-group-item">
        <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado" :id="tarefa.titulo" type="checkbox">
        <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
          {{ tarefa.titulo }}
        </label>
      </li>
    </ul>
  </div>
</template>

<style scoped>
  .done {
    text-decoration: line-through;
  }
</style>
