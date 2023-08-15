<script setup>
    const props = defineProps(['tarefas', 'tarefasFiltro', 'tarefasPendentes'])
</script>

<template>
    <ul v-if="props.tarefasFiltro > 0" class="list-group mt-4" v-for="tarefa in props.tarefas">
        <li class="list-group-item">
            <input @change="evento => tarefa.finalizado = evento.target.checked" :checked="tarefa.finalizado"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
    <span v-else class="tarefas-status">
        Não tem tarefas<span v-if="props.tarefasPendentes > 0"> Finalizadas</span>.
    </span>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }
</style>