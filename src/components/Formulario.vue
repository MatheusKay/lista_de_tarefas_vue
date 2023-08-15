<script setup>
    const props = defineProps(['cadastraTarefa', 'tarefaNova', 'trocraFiltro', 'editaTarefaNova'])
</script>

<template>
    <form @submit.prevent="props.cadastraTarefa" class="mt-4">
        <div class="row">
            <div class="col">
                <input :value ="props.tarefaNova" @change="props.editaTarefaNova" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control mb-3">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.trocraFiltro" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Tarefas pendentes</option>
                    <option value="finalizadas">Tarefas finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>