<script setup>
    import { reactive, computed } from "vue";
    import Cabecalho from "./components/Cabecalho.vue";
    import Form from "./components/Form.vue";
    import ListadeTarefas from "./components/ListadeTarefas.vue"

    

    const estado = reactive({
        filtro: "all", //para trabalhar com a filtragem das options(html)
        tarefaTemp: "", //para adicionar tarefa com submit
        tarefas: [
            {
                titulo: "Study ES6",
                finalizada: false,
            },
            {
                titulo: "Study SASS",
                finalizada: false,
            },
            {
                titulo: "Study JS",
                finalizada: true,
            },
            {
                titulo: "Study Python",
                finalizada: false,
            },
            {
                titulo: "Study VueJS",
                finalizada: true,
            },
        ],
    });
    //filtrando tarefas nao finalizadas
    const getTarefasPendentes = () => {
        return estado.tarefas.filter((tarefa) => !tarefa.finalizada);
    };
    //filtrando tarefas finalizadas
    const getTarefasFinalizadas = () => {
        return estado.tarefas.filter((tarefa) => tarefa.finalizada);
    };
//condicoes para os item de cada item da filtragem (pendentes, finalizadas e todas)
    const getTarefasFiltradas = () => {
        const { filtro } = estado;
        switch (
            filtro //filtro='all'
        ) {
            case "to-do": //<option value='to-do'>
                return getTarefasPendentes();
            case "completed": //<option value='completed'>
                return getTarefasFinalizadas();
            default:
                return estado.tarefas;
        }
    };

    //condicao que faz aparecer TASK ou TASKS
    const taskOrTasks = computed(() => {
    return getTarefasPendentes().length > 1 ? "tasks" : "task";
    //"?" eh um operador ternario que funciona como if/else
    });
    // função para atualizar o filtro
    const updateFiltro = (evento) => {
        estado.filtro = evento.target.value;
    };

    //CADASTRAR TAREFA NOVA NO SUBMIT do FORM
    const cadastrarTarefa = () => {
        const tarefaNova = {
            titulo: estado.tarefaTemp,
            finalizada: false, //comeca com tarefa pendente
        };
        estado.tarefas.push(tarefaNova); //para adicionar nova tarefa
        estado.tarefaTemp = ""; //para limpar a tarefa do input apos registrada
    };
</script>

<template>
    <div class="container">
        <Cabecalho :tarefas-pendentes="getTarefasPendentes().length" :task-or-tasks="taskOrTasks"></Cabecalho>
        <Form :trocar-filtro="evento=>estado.filtro=evento.target.value":tarefa-tempo="estado.tarefaTemp" :editar-tarefa-temp="evento=>estado.tarefaTemp=evento.target.value" :cadastrar-tarefa="cadastrarTarefa"></Form>
        <ListadeTarefas :tarefas-filter="getTarefasFiltradas()"></ListadeTarefas>
        </div>
</template>


