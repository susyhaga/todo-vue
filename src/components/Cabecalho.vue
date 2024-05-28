<script setup>

const props= defineProps(['tarefasPendentes', 'taskOrTasks', 'colorTarefasPend'])

</script>

<template>
    <header class="p-5 mb-4 mt-4 rounded-3" id="colorheader">
        <h1>My tasks</h1>

        <h4> You have <span :class="{textcolor:props.tarefasPendentes}">{{ props.tarefasPendentes}}</span> pending {{props.taskOrTasks}}</h4>
    </header>
</template>
<style scoped>
    #colorheader {
        background-color: rgb(211, 202, 202);
    }
    .textcolor{
        color: rgb(225, 24, 24);
    }
</style>