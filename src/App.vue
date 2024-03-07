<script setup>
  import { reactive } from 'vue';
  import Header from './components/Header.vue';
  import Form from './components/Form.vue';
  import TaskList from './components/TaskList.vue';

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

  const getPendingTask = () => {
    return estado.tarefas.filter(tarefa => !tarefa.finalizada)
  }

  const getTaskFinished = () => {
    return estado.tarefas.filter(tarefa => tarefa.finalizada)
  }
  
  const getTaskFilters = () => {
    const { filter } = estado;
    switch(filter) {
      case 'pendentes':
        return getPendingTask();
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
    <Header :-pending-task="getPendingTask().length" />
    <Form :change-filter="evento => estado.filter = evento.target.value" :temporary-task="estado.temporaryTask" :change-task-temp="evento => estado.temporaryTask = evento.target.value" :new-task="newTask"/>
    <TaskList :task="getTaskFilters()"/>
  </div>
</template>