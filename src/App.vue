<script setup>
    import { reactive, computed} from 'vue';


//criar um estado (reactive) com tarefas
    const estado = reactive({
        filtro:"all", //para trabalhar com a filtragem das options(html)
        tarefaTemp:'', //para adicionar tarefa com submit
        tarefas:[
            {
                titulo:"Study ES6",
                finalizada: false,
            },
            {
                titulo:"Study SASS",
                finalizada: false,
            },
            {
                titulo:"Study JS",
                finalizada: true,
            },
            {
                titulo:"Study Python",
                finalizada: false,
            },
            {
                titulo:"Study VueJS",
                finalizada: true,
            }
        ]
    });
    //filtrando tarefas nao finalizadas 
    const getTarefasPendentes = () => {
        return estado.tarefas.filter(tarefa => !tarefa.finalizada)
    }
       //filtrando tarefas finalizadas 
    const getTarefasFinalizadas = () => {
        return estado.tarefas.filter(tarefa => tarefa.finalizada)
    }
    //condicoes para os item de cada item da filtragem (pendentes, finalizadas e todas)
    const getTarefasFiltradas = () => {
        const { filtro } = estado;
        switch (filtro) { //filtro='all'
            case 'to-do'://<option value='to-do'>
                return getTarefasPendentes();
            case 'completed'://<option value='completed'>
                return getTarefasFinalizadas();
            default:
                return estado.tarefas;
        }
    }
    //condicao que faz aparecer TASK ou TASKS

const tasksOrTask = computed(() => {
    return getTarefasPendentes().length > 1 ? "tasks" : "task"; 
    //"?" eh um operador ternario que funciona como if/else
});
// função para atualizar o filtro
const updateFiltro = (evento) => {
    estado.filtro = evento.target.value;
};

//CADASTRAR TAREFA NOVA NO SUBMIT do FORM
const cadastrarTarefa = () =>{
    const tarefaNova = {
        titulo: estado.tarefaTemp,
        finalizada:false, //comeca com tarefa pendente
    }
    estado.tarefas.push(tarefaNova); //para adicionar nova tarefa
    estado.tarefaTemp =''; //para limpar a tarefa do input apos registrada
}
</script>

<template>
    <!-- CABECALHO -->
<div class="container">
    <header id="colorheader" class="p-5 mb-4 mt-4 rounded-3">
            <h1>My tasks</h1>
            <h4>
                You have <span class="red-text">{{getTarefasPendentes().length}}</span> pending {{ tasksOrTask }}
            </h4>
    </header>
    <!-- FORMULARIO -->
    <form @submit.prevent="cadastrarTarefa">   
        <!--prevent eh o prevent.default... todo SUBMIT precisa  -->
        <div class="container">
            <div class="row">
                <div class="col">
                    <input :value="estado.tarefaTemp" @change="evento=>estado.tarefaTemp=evento.target.value" required type="text" class="form-control" placeholder="Type task description">
                        <!-- :value… para limpar o campo que a tarefa foi digitada-->
                </div>
                <div class="col-md-2">
                    <button class="btn btn-primary">Register</button>
                </div>
                <div class="col md-2">
                    <select @change="updateFiltro" class="form-control">
                        <!-- option cria um filtro das tarefas q serao exibidas -->
                        <option value="all"> All tasks</option>
                        <option value="to-do">To-do</option>
                        <option value="completed">Completed</option>
                    </select>
                </div>
            </div>
        </div>
    </form>
            <!-- {{ estado.filtro }} teste de renderizacao do filtro -->

        <!-- Lista nao ordenada de tarefas -->
        <ul class="list-group mt-4">
            <li class="list-group-item" v-for="tarefa in getTarefasFiltradas()">
                <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
                <!-- o checkbox sera marcado quando a tarefa.finalizada for TRUE  
                    por causa da PROPRIEDADE checked-->
                <label :class="{done:tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
                {{tarefa.titulo}} 
                </label>
            </li>
        </ul>
    </div>
</template>

<style scoped>
#colorheader{
    background-color: rgb(211, 202, 202);
}
.done{
    text-decoration: line-through;
}

.red-text{
    color:rgb(150, 6, 6);
    font-size: 30px;
}
</style>
