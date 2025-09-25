<script setup>
import { onMounted, ref } from 'vue';

    let texto = ref('Hello Wolrd')

    onMounted(() =>{
        setTimeout(() =>{
            texto.value = 'Alterando texto' /* setTimeout faz com que o texto modifque apos 3 segundos*/
        }, 3000)
    })
</script>

<template>
    <h1>{{texto}}</h1>
</template>