<script setup>
const props = defineProps(['propsTarefasFiltradas'])

</script>

<template>
    <ul class="list-group mt-4">

        <li class="list-group-item" v-for="tarefa in props.propsTarefasFiltradas">
            <!-- <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()"> -->


            <input :id="tarefa.titulo" type="checkbox" :checked="tarefa.finalizada"
                @change="evento => tarefa.finalizada = evento.target.checked">

            <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-3">
                {{ tarefa.titulo }}
            </label>

        </li>

    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>