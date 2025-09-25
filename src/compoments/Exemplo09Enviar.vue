<script setup>
    function validaFormulario(event){
        alert('Formulario enviado')
        event.preventDefault();
    }
</script>


<template>
    <form action="https://www.google.com" @submit="validaFormulario">
        <input type="submit" value="Enviar formulario" > <!-- evento para enviar  -->
    </form>
</template>