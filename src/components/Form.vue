<script setup>
    const props=defineProps(['cadastrarTarefa', 'tarefaTempo', 'trocarFiltro', 'editarTarefaTemp'])
</script>

<template>
    <form @submit.prevent="props.cadastrarTarefa">  
        <!--prevent eh o prevent.default... todo SUBMIT precisa  -->
        <div class="row">
            <div class="col">
                <input :value="props.tarefaTempo" @change="props.editarTarefaTemp" required type="text" placeholder="Type the task description"  class="form-control">
                    <!-- :value… para limpar o campo que a tarefa foi digitada-->
            </div>
            <div class="col-md-2">
                <button class="btn btn-primary ms-0">Register</button>
            </div>
            <div class="col md-2">
                <select @change="props.trocarFiltro" class="form-control">
                    option cria um filtro das tarefas q serao exibidas 
                    <option value="all"> All tasks</option>
                    <option value="to-do">To-do</option>
                    <option value="completed">Completed</option>
                </select>
            </div>
        </div>
    </form>
</template>