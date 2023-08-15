<script setup>
    const props = defineProps(['getTarefasFiltro', 'tarefaFinalizada'], )
</script>

<template>
    <ul class="list-group mt-4" v-for="tarefa in props.getTarefasFiltro">
        <li class="list-group-item">
            <input @change="props.tarefaFinalizada"
                :id="tarefa.titulo" type="checkbox">
            <label :class="{ done: tarefa.finalizado }" class="ms-3" :for="tarefa.titulo">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>