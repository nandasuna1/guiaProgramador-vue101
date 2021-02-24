<template>

  <div id="app"><div class="buttons">
  <button class="button is-primary">Primary</button>
  <button class="button is-link">Link</button>
</div>
    <h3>Cadastro: </h3>
    
    <p v-show="erro">o nome é invalido</p>
    <input type="text" placeholder="nome" v-model="nomeField"><br>
    <input type="text" placeholder="email" v-model="emailField"><br>
    <input type="number" placeholder="idade" v-model="idadeField"><br>
    <button @click="cadastrarUsuario()">cadastrar</button>
    <h1>Guia de Clientes</h1>
    <div v-for="(cliente) in orderClientes" :key="cliente.id">
      <Cliente :cliente="cliente" @meDelete="deletarUsuario($event)"/>
      <hr>
    </div>

  </div>
</template>

<script>
import Cliente from './components/Cliente';
//import Produto from './components/Produtos';
import _ from 'lodash';


export default {
  name: 'App',
  data(){
    return{
      erro: false,
      nomeField: "",
      emailField:"",
      idadeField: 0,
      
      clientes: [
      {
        nome: 'Fernanda',
        email: "nanda@teste.com",
        idade: 20,
        id: 1,
      },
      {
        nome: 'jose',
        email: 'jose@teste.com',
        idade: 19,
        id: 2,
      },
    ]
    }
    
  },
  components: {
    Cliente,
    //Produto
  },
  methods: {
    cadastrarUsuario: function(){
      if(this.nomeField == "" || this.nomeField == " " || this.nomeField.lenght < 3){
        this.erro = true
        window.alert("Informações invalidas")
        
      }
      else{
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeField, id: Date.now()})
        this.nomeField = ""
        this.emailField = ""
        this.idadeField = 0
        this.erro = false
      }
    },
    deletarUsuario: function($event){
          var id = $event.idDoCliente;
          var novalista = this.clientes.filter(cliente => cliente.id != id);
          this.clientes = novalista;
    }
  },
  computed:{
    orderClientes: function(){
      return _.orderBy(this.clientes, ['nome'], ['asc']);
    }
  }
}
</script>

<style>
#app {
margin: 0;
}
hr{
  background: black;
}
</style>
