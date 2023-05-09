<script setup>
const props = defineProps(["tarefas"]);
</script>

<template>
  <ul v-if="props.tarefas.length > 0" class="list-group mt-4">
    <li class="list-group-item" v-for="tarefa in props.tarefas">
      <input
        @change="(evento) => (tarefa.finalizada = evento.target.checked)"
        type="checkbox"
        :checked="tarefa.finalizada"
        :id="tarefa.título"
      />
      <label
        :class="{ done: tarefa.finalizada }"
        class="ms-3"
        :for="tarefa.título"
        >{{ tarefa.título }}</label
      >
    </li>
  </ul>
  <p class="mt-3" v-else>Nenhuma tarefa encontrada</p>
</template>

<style scoped>
.done {
  text-decoration: line-through;
}
</style>
