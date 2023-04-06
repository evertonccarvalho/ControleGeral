<template>
  
    <div class="container"> 
      <h1>SSA2</h1>
      <br>
      <form class="row g-3">
        <div class="col">
          <input type="text" class="form-control" placeholder="Responsavel" aria-label="Responsavel" v-model="nomeField">
        </div>
        <div class="col">          
          <select id="ubs" class="form-select">
            <option selected>UBS</option>
            <option>Sede I</option>
            <option>Sede II</option>
            <option>Batoque</option>
            <option>Baixa da Umburana</option>
            <option>Baixio Grande</option>
            <option>Castanhão</option>
            <option>Tibolo</option>
          </select>
        </div>
        <div class="row g-3">
          <div class="col">
            <label>Crianças até 6 meses</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="criancasMenor6Meses">
          </div>

          <div class="col">
            <label>Crianças em AME</label>
            <input class="form-control" type="number" placeholder="Crianças em AME" v-model="criancaAme">
          </div>

          <div class="col">
            <label>Crianças até 2 Anos</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="criancas2Anos">
          </div>
        </div>
        <div class="row g-3">
          <div class="col"> 
            <label>Gestantes</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="gestantes">
          </div>

          <div class="col"> 
            <label>Gestante Menor de 20 Anos</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="gestantesAte20Anos">
          </div>
        </div>
        <div class="row g-3">

          <div class="col">
            <label>Total de Familias Acompanhadas</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="familias">
          </div>

          <div class="col">  
            <label>Visitas Domiciliar ACS / Outros Profissionais</label>
            <input class="form-control" type="number" placeholder="Crianças < 6 Meses" v-model="familiasAcompanhada">
          </div>
          
        </div>
          
      </form>  
      <div class="enviar">
        <div class="form-check">
          <input class="form-check-input" type="checkbox" id="gridCheck">
          <label class="form-check-label" for="gridCheck">
            Marque
          </label>
        </div>
        <button class="btn btn-primary" @click="cadastrarUsuario">Cadastrar</button>
        <small id="nome-erro" v-show="deuErro"> Nome invalido tente novamente</small>
      </div>
      <hr>
      <div v-for="(cliente,index) in orderClientes" :key="cliente.id">
        <h4>{{ index +1 }}</h4>
        <Cliente :cliente="cliente" :showIdade="true" @meDelete="deletarUsuario ($event)"/>
      </div>
    </div>
</template>

<script>
import _ from 'lodash';
import Cliente from './Cliente.vue'
export default {  data(){
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
  .container{
    padding-top: 10%;
    padding-bottom:10% ;
  }
</style>