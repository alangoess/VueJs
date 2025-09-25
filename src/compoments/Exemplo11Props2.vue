<script setup>
    const props = defineProps(['nome', 'idade', 'cidades', 'funcao'])
</script>

<template>
    Nome: {{ nome }}
    Idade: {{ idade }}
    
    <ul>
        <li v-for="cidade in cidades">
            {{ cidade }}
        </li>
    </ul>

    <button @click="funcao"></button> <!-- busca o alert do nome :funcao='mensagem' -->
</template>