<script setup>
    const props = defineProps(['newTask', 'temporaryTask', 'changeFilter', 'changeTaskTemp'])
</script>

<template>
    <form @submit.prevent="props.newTask" >
        <div class="row">
            <div class="col">
                <input :value="props.temporaryTask" @change="props.changeTaskTemp" required type="text" placeholder="Digite aqui a descrição da tarefa" class="form-control">
            </div>
            <div class="col-md-2">
                <button type="submit" class="btn btn-primary">Cadastrar</button>
            </div>
            <div class="col-md-2">
                <select @change="props.changeFilter" class="form-control">
                    <option value="todas">Todas tarefas</option>
                    <option value="pendentes">Pendentes</option>
                    <option value="finalizadas">Finalizadas</option>
                </select>
            </div>
        </div>
    </form>
</template>