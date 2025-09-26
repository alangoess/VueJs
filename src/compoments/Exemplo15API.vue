<script setup>
import { onMounted, ref } from 'vue';

    let produtos = ref([]) //Serve pra guardar a lista de produtos vindos do backend.

    //visibilidade dos botoes
    let btnCadastrar = ref(true)


    onMounted(() =>{
       fetch('http://localhost:3000/produtos') //faz uma requisição GET para pegar os produtos do servidor.
       .then(response => response.json())
       .then(data => produtos.value = data) //resultado já convertido:
    })

     let obj = ref({id:0, nome:'', preco:0, estoque:0});


    function enviar(event){

        fetch('http://localhost:3000/produtos', { //quando trabalhar com put, post ou delete, temos que especificar no fetch um segundo parametro
            method:'POST',
            body:JSON.stringify(obj.value), //converter objeto para texto JSON
            headers:{'Content-Type':'application/json'} //especificar o tipo de dado esta sendo manipulado para efetuar a requisiçao

        })
        .then(response => response.json())
        .then(data => {
            //cadastrar produto no vetor
            produtos.value.push(data)

            //limpar input
            obj.value.produto = ''
            obj.value.valor = 0
        })

        event.preventDefault() //previne que a pagina seja atualizada apos clicar no ok do alert
    }

    function editar(){

        fetch(`http://localhost:3000/produtos/${obj.value.id}`, { //quando trabalhar com put, post ou delete, temos que especificar no fetch um segundo parametro
            method:'PUT', //metodo para o update
            body:JSON.stringify(obj.value), //converter objeto para texto JSON
            headers:{'Content-Type':'application/json'} //especificar o tipo de dado esta sendo manipulado para efetuar a requisiçao

        })
        .then(response => response.json())
        .then(data => {

            //obter o indice do vetor 
            let indiceProduto = produtos.value.findIndex(objP =>{
                return objP.id === data.id
            }) //obj para representar valor de cada linha no parametro

            //editar produto no vetor
            produtos.value[indiceProduto] = data

            //limpar input
            obj.value.id = 0
            obj.value.produto = ''
            obj.value.valor = 0
        })

    }

    function remover(){

        fetch(`http://localhost:3000/produtos/${obj.value.id}`, { //quando trabalhar com put, post ou delete, temos que especificar no fetch um segundo parametro
            method:'DELETE', //metodo para o update
            headers:{'Content-Type':'application/json'} //especificar o tipo de dado esta sendo manipulado para efetuar a requisiçao

        })
        .then(response => {
    if (!response.ok) throw new Error('Erro ao deletar');
})
        .then(() => {

            //obter o indice do vetor 
            let indiceProduto = produtos.value.findIndex(objP =>{
                return objP.id === obj.value.id
            }) //obj para representar valor de cada linha no parametro

            //remover produto no vetor
            produtos.value.splice(indiceProduto, 1)

            
        })

    }

//funcao para selecionar um produto especifico
    function selecionar(indice){
        obj.value = {
            id: produtos.value[indice].id,
            nome: produtos.value[indice].nome,
            preco: produtos.value[indice].preco,
            estoque: produtos.value[indice].estoque
        }

        btnCadastrar = false
    }
</script>

<style>
    form{
       width: 50%; 
       margin: 50px auto;
       text-align: center;
    }

    input{
        margin-bottom: 10px;
    }

    .btnEspacamento{
        margin-left: 5px;
        margin-right: 5px;
    }
</style>

<template>

    <form @submit="enviar">
        
        <input type="hidden" v-model="obj.id">
        <input type="text" placeholder="Nome" class="form-control" v-model="obj.nome" >
        <input type="number" placeholder="Nome" class="form-control" v-model="obj.preco">
        <input type="number" placeholder="Estoque" class="form-control" v-model="obj.estoque">
        <button type="submit" v-if="btnCadastrar" class="btn btn-primary">Cadastrar</button>
        <button @click="editar" class="btn btn-primary btnEspacamento" v-if="!btnCadastrar">Edtitar</button>
        <button @click="remover" class="btn btn-primary" v-if="!btnCadastrar">Exlcuir</button>
    </form>

    <table class="table table-striped">
        <thead>
            <tr>
                <th>Nome</th>
                <th>Preço</th>
                <th>Estoque</th>
            </tr>
        </thead>

        <tbody>
            <tr v-for="(produto, indice) in produtos">
                <td>{{ produto.nome }}</td>
                <td>{{ produto.preco }}</td>
                <td>{{ produto.estoque }}</td>
                <td><button @click="selecionar(indice)" class="btn btn-primary">Selecionar</button></td>
            </tr>
        </tbody>
    </table>
</template>