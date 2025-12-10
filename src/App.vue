<script setup>
import { reactive } from 'vue';

const estado = reactive({
  filtro: 'todas',
  tarefaTem: ''
  ,
  tarefas: [
    {
      titulo: 'Estudar ES6',
      finalizada: false,

    }, {
      titulo: 'Estudar SASS',
      finalizada: false,
    }, {
      titulo: 'Ir para academia',
      finalizada: true,
    }

  ]
})

const getTarefasPendentes = () => {
  return estado.tarefas.filter(tarefa => !tarefa.finalizada)
}

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter(tarefa => tarefa.finalizada)
}

const getTarefasFiltradas = () => {
  const { filtro } = estado;
  switch (filtro) {
    case 'pendentes':
      return getTarefasPendentes();
    case 'finalizadas':
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
}

const cadastraTarefa = () => {
  const tarefaNova = {
    titulo: estado.tarefaTem,
    finalizada: false
  }
  estado.tarefas.push(tarefaNova)
  estado.tarefaTem=""
}


</script>

<template>

  <div class="container">
    <!-- ---------------------------------------------------- -->
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>minhas tarefas </h1>
      <p>você possui {{ getTarefasPendentes().length }} tarefas pendentes</p>

    </header>
    <!-- ----------------------------------------------------------------- -->
    <form @submit.prevent="cadastraTarefa">

      <div class="row">
        <!-- -------- -->

        <div class="col">
          <input :value="estado.tarefaTem" @change="evento => estado.tarefaTem = evento.target.value" required type="text"
            placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>


        <div class="col-md-1">
          <button type="submite" class="btn btn-primary">Cadastrar</button>
        </div>

        <div class="col-md-2">
          <select @change="evento => estado.filtro = evento.target.value" class="form-control">
            <option value="todas">Todas as tarefas</option>
            <option value="pendentes">Tarefas pendenstes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>

        <!-- ----------------- -->
      </div>
    </form>
    <!-- ------------------------------------------------------------------ -->
    <ul class="list-group mt-4">

      <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">

        <input :id="tarefa.titulo" type="checkbox" :checked="tarefa.finalizada"
          @change="evento => tarefa.finalizada = evento.target.checked">

        <label :class="{ done: tarefa.finalizada }" :for="tarefa.titulo" class="ms-3">
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
