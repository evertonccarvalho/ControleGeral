<template>
  <Navbar/>
  <div id="app">
    <div class="container">
      <h3>Cadastro</h3>
      <form class="row g-3">
        <div class="col">
          <input type="text" class="form-control" placeholder="First name" aria-label="First name">
        </div>
        <div class="col">
          
          <select id="ubs" class="form-select">
            <option selected>UBS</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
          </select>
        </div>


        <input class="form-group mb-3" type="text" placeholder="Responsavel" v-model="nomeField">        
        <div class="ccol-md-6">
          <label for="SelectUBS" class="form-label">UBS</label>
          <select id="ubs" class="form-select">
            <option selected>UBS</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
            <option>Baixio Grande</option>
          </select>
          
          <div class="col-md-6">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="criancasMenor6Meses">
            <input class="form-group" type="number" placeholder="Crianças em AME" v-model="criancaAme">
          </div>
          <div class="col">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="criancas2Anos">
          </div>
          <div class="col">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="gestantes">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="gestantesAte20Anos">
          </div>
          <div class="col">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="familias">
            <input class="form-group" type="number" placeholder="Crianças < 6 Meses" v-model="familiasAcompanhada">
          </div>


       
          
        </div>    
      </form>  
      <div class="form-check">
      <input class="form-check-input" type="checkbox" id="gridCheck">
      <label class="form-check-label" for="gridCheck">
        Check me out
      </label>
      </div>
      
      <button class="btn btn-primary" @click="cadastrarUsuario">Cadastrar</button>
      <small id="nome-erro" v-show="deuErro"> Nome invalido tente novamente</small>
      

      <hr>

      <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
        <h4>{{ index +1 }}</h4>
        <Cliente :cliente="cliente" :showIdade="true" @meDelete="deletarUsuario ($event)"/>

      </div>
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
      criancasMenor6Meses:0,
      criancaAme:0,
      criancas2Anos:0,
      gestantes: 0,
      gestantesAte20Anos:0,
      familias:0,
      familiasAcompanhada:0,
      
      clientes: [
        {
          id: 1,
          nome: "Everton Carvalho",
          criancas6meses: 0,
          criancaAme: 0,
          criancas2Anos: 0,
          gestantes: 0,
          gestantesAte20Anos:0,
          familias:0,
          familiasAcompanhada:0,
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
      if(this.nomeField == "" || this.nomeField == "" || this.nomeField == "" || this.nomeField ==" " || this.nomeField ==" "< 0){
        this.deuErro = true;

      }else{
        this.clientes.push({nome: this.nomeField, criancas6meses: this.criancasMenor6Meses, criancaAme: this.criancaAme, criancas2Anos: this.criancas2Anos, gestantes: this.gestantes, gestantesAte20Anos: this.gestantesAte20Anos, familias: this.familias, familiasAcompanhada: this.familiasAcompanhada})
        this.nomeField="";
        this.criancasMenor6Meses=0;
        this.criancaAme=0;
        this.criancas2Anos= 0;
        this.gestantes= 0;
        this.gestantesAte20Anos=0;
        this.familias=0;
        this.familiasAcompanhada=0;
        
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
            return _.orderBy(this.clientes,['id'],['asc']);
    }
  }
}
</script>

<style>
  #nome-erro{
    color: red;
  }
</style>
