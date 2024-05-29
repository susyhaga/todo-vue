<script setup>
    const props=defineProps(['tarefasFilter'])
</script>
<template>
    <ul v-if= "props.tarefasFilter.length > 0"class="list-group mt-4">
        <li class="list-group-item" v-for="tarefa in props.tarefasFilter">
            <input @change="evento => tarefa.finalizada = evento.target.checked" :checked="tarefa.finalizada" :id="tarefa.titulo" type="checkbox">
            <!-- o checkbox sera marcado quando a tarefa.finalizada for TRUE  por causa da PROPRIEDADE checked-->
            <label :class="{done:tarefa.finalizada}" class="ms-3" :for="tarefa.titulo">
            {{tarefa.titulo}}
            </label>
        </li>
    </ul>
    <div v-else class="mt-4">
        <h2>No pending task at the moment</h2>
    </div>
</template>

<style scoped>
    .done {
        text-decoration: line-through;
    }

</style>
