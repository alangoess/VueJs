<script setup>
    import Exemplo11Props2 from './Exemplo11Props2.vue';
    let cidades = ['Sao paulo', 'Salvador', 'Recife']

    function mensagem(){
        alert('teste')
    }
</script>

<template>
    <Exemplo11Props2 nome="Alan" idade="24" :cidades="cidades" :funcao="mensagem"></Exemplo11Props2>
</template>