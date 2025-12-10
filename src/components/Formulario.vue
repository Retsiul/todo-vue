<script setup>
const props = defineProps (['propCadastraTarefa','propTarefaTem','trocarFiltro','editaTarefaTem'])

</script>

<template>

    <form @submit.prevent="props.propCadastraTarefa">
    <!-- <form @submit.prevent="cadastraTarefa"> -->

        <div class="row">
            <!-- -------- -->

            <div class="col">
                <input :value="props.propTarefaTem" @change="props.editaTarefaTem" required
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
                <!-- <input :value="estado.tarefaTem" @change="evento => estado.tarefaTem = evento.target.value" required
                    type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control"> -->
            </div>


            <div class="col-md-1">
                <button type="submite" class="btn btn-primary">Cadastrar</button>
            </div>

            <div class="col-md-2">
                <select @change="props.trocarFiltro" class="form-control">

                <!-- <select @change="evento => estado.filtro = evento.target.value" class="form-control"> -->
                    <option value="todas">Todas as tarefas</option>
                    <option value="pendentes">Tarefas pendenstes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>

            <!-- ----------------- -->
        </div>
    </form>
</template>