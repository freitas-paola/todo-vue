<script setup>
import { reactive } from "vue";
import Header from "./components/Header.vue";
import Form from "./components/Form.vue";
import TasksList from "./components/TasksList.vue";

const estado = reactive({
  filtro: "todas",
  tarefaTemp: "",
  tarefas: [
    {
      título: "Estudar ES6",
      finalizada: false,
    },
    {
      título: "Estudar SASS",
      finalizada: true,
    },
    {
      título: "Estudar React",
      finalizada: false,
    },
  ],
});

const getTarefasPendentes = () => {
  return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
};

const getTarefasFinalizadas = () => {
  return estado.tarefas.filter((tarefa) => tarefa.finalizada);
};

const getTarefasFiltradas = () => {
  const { filtro } = estado;

  switch (filtro) {
    case "pendentes":
      return getTarefasPendentes();
    case "finalizadas":
      return getTarefasFinalizadas();
    default:
      return estado.tarefas;
  }
};

const cadastraTarefa = () => {
  const novaTarefa = {
    título: estado.tarefaTemp,
    finalizada: false,
  };

  estado.tarefas.push(novaTarefa);
  estado.tarefaTemp = "";
};
</script>

<template>
  <div class="container">
    <Header :tarefas-pendentes="getTarefasPendentes().length" />
    <Form
      :tarefa-temp="estado.tarefaTemp"
      :edita-tarefa-temp="(evento) => (estado.tarefaTemp = evento.target.value)"
      :cadastra-tarefa="cadastraTarefa"
      :trocar-filtro="(evento) => (estado.filtro = evento.target.value)"
    />
    <TasksList :tarefas="getTarefasFiltradas()" />
  </div>
</template>
