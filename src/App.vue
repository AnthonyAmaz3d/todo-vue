<script setup>
import { reactive } from 'vue';

  const estado = reactive({
    filter: 'todas',
    temporaryTask: '', 
    tarefas: [
      {
        titulo: 'Estudar ES6',
        finalizada: false,
      },
      {
        titulo: 'Estudar Python',
        finalizada: false,
      },
      {
        titulo: 'Ir para academia',
        finalizada: true,
      }
    ]
  })

  const getTaskPending = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTaskFinished = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }
  
  const getTaskFilters = () => {
    const { filter } = estado;
    switch(filter) {
      case 'pendentes':
        return getTaskPending();
      case 'finalizadas':
        return getTaskFinished();
      default: 
        return estado.tarefas;
    }
  }


  const newTask = () => {
    const newTask = {
      titulo: estado.temporaryTask,
      finalizada: false,
    }
    estado.tarefas.push(newTask);
    estado.temporaryTask = '';
  }
</script>

<template>
  <div class="container">
    <header class="p-5 mb-4 mt-4 bg-light rounded-3">
      <h1>Minhas Tarefas</h1>
      <p>
        Você possui {{ getTaskPending().length }} tarefas pendentes
      </p>
    </header>
    <form @submit.prevent="newTask()" >
      <div class="row">
        <div class="col">
          <input :value="estado.temporaryTask" @change="evento => estado.temporaryTask = evento.target.value" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
        </div>
        <div class="col-md-2">
          <button type="submit" class="btn btn-primary">Cadastrar</button>
        </div>
        <div class="col-md-2">
          <select @change="evento => estado.filter = evento.target.value" class="form-control">
            <option value="todas">Todas tarefas</option>
            <option value="pendentes">Pendentes</option>
            <option value="finalizadas">Finalizadas</option>
          </select>
        </div>
      </div>
    </form>
    <ul class="list-group mt-4">
      <li class="list-group-item" v-for="tarefa in getTaskFilters()" >
        <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox" >
        <label class="ms-3" :class="{ done: tarefa.finalizada}" :for="tarefa.titulo">
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
