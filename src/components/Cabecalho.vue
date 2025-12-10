<script setup>
 const props = defineProps(['tarefasPendentes'])

</script>

<template>
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
        <h1>minhas tarefas </h1>
        <p>você possui {{ props.tarefasPendentes }} tarefas pendentes</p>
      
        <!-- <p>você possui {{ getTarefasPendentes().length }} tarefas pendentes</p> -->

    </header>
</template>