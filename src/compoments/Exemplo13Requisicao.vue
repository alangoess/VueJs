<script setup>
import { onMounted, ref } from 'vue';

    let vetor = ref([])

    onMounted(() =>{
        fetch('https://jsonplaceholder.typicode.com/posts')
        .then(response => response.json())
        .then(response => vetor.value = response)
    })
</script>

<template>

<table>
    <tr v-for="v in vetor" >
        <td>{{ v.id }}</td>
        <td>{{ v.title }}</td>
        <td>{{ v.body }}</td>
        <td>{{ v.userId }}</td>
    </tr>
</table>
</template>