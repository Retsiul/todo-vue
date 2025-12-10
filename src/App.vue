<script setup>
import { reactive } from 'vue';
import Cabecalho from './components/Cabecalho.vue';
import Formulario from './components/Formulario.vue';
import ListaDeTarefas from './components/ListaDeTarefas.vue';


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
  estado.tarefaTem = ""
}


</script>

<template>

  <div class="container">
    <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" />
    <Formulario :prop-cadastra-tarefa="cadastraTarefa" :prop-tarefa-tem="estado.tarefaTem"
      :edita-tarefa-tem="evento => estado.tarefaTem = evento.target.value"
      :trocar-filtro="evento => estado.filtro = evento.target.value" />

    <ListaDeTarefas :props-tarefas-filtradas="getTarefasFiltradas()" />
  </div>
</template>


