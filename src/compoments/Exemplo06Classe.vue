<script setup>
    let validacao = true;
</script>

<style>
    .ok{
        color: green;
    }

    .falha{color: red;}
</style>

<template>
    <p :class="validacao ? 'ok' : 'falha'">Utilizando a diretiva class</p>

</template>