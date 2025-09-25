<script setup>
    function mensagem(){
        alert('executando')
    }
</script>

<template>
    <input type="text" @keyup.enter="mensagem()">  <!-- usado para quando a pessoa digitar um caractere especifico ou uma tecla -->
</template>