<script setup>
    const props = defineProps(['tarefasPendentes'])
</script>
<template>
    <header class="p-5 md-4 mt-4 bg-light rounded-3">
        <h1>Minhas tarefas</h1>
        <p>
            Voce possui {{ props.tarefasPendentes }} tarefas pendentes
        </p>
    </header>
</template>