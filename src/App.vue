<template>
  <Navbar/>
  <div id="app">

    <h3>Cadastro</h3>
    
    <input type="text" placeholder="nome" v-model="nomeField">
    <input type="text" placeholder="email" v-model="emailField">
    <input type="number" placeholder="idade" v-model="idadeField">
    
    <button @click="cadastrarUsuario">Cadastrar</button>
    <small id="nome-erro" v-show="deuErro"> Nome invalido tente novamente</small>
    

    <hr>

    <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
      <h4>{{ index +1 }}</h4>
      <Cliente :cliente="cliente" :showIdade="true" @meDelete="deletarUsuario ($event)"/>

    </div>
  </div>

  
  
</template>

<script>
import _ from 'lodash';
import Cliente from './components/Cliente';
import Navbar from './components/Navbar';
//import Produto from './components/Produto.vue'

export default {
  name: 'App',
  data(){
    return{
      deuErro: false,
      nomeField:"",
      emailField:"",
      idadeField:0,
      
      clientes: [
        {
          id: 1,
          nome: "Éverton Carvalho",
          email: "evertonsnake@gmail.com",
          idade: 32
        }
      ]
    }
  },
  components: {
    Cliente, 
    Navbar,
    //Produto
  },
  methods:{
    cadastrarUsuario: function(){
      if(this.nomeField == "" || this.nomeField == "   " || this.nomeField.length < 3){
        this.deuErro = true;

      }else{
        this.clientes.push({nome: this.nomeField, email: this.emailField, idade: this.idadeFiel, id: Date.now()})
        this.nomeField="";
        this.emailField="";
        this.idadeField= 0;
      }
    },
    deletarUsuario: function($event){
      console.log("receendo evento");
      var id = $event.idDoCliente;
      var novoArray = this.clientes.filter(cliente => cliente.id != id);
      this.clientes = novoArray;
      
    }
  },
  computed: {
    orderClientes: function(){
            return _.orderBy(this.clientes,['nome'],['asc']);
    }
  }
}
</script>

<style>
  #nome-erro{
    color: red;
  }
</style>
