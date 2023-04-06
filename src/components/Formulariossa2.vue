<template>
  <Navbar/>
  <div id="app">
    <div class="container"> 
      <h1>Cadastro</h1>
      <br>
      <form class="row g-3">
        <div class="col">
          <input type="text" class="form-control" placeholder="Responsavel" aria-label="Responsavel" v-model="nomeField">
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
            Check me out
          </label>
        </div>
        <button class="btn btn-primary" @click="cadastrarUsuario">Cadastrar</button>
        <small id="nome-erro" v-show="deuErro"> Nome invalido tente novamente</small>
      </div>
      <hr>
      <div v-for="(Formulariossa2,index) in orderFormulariossa2s" :key="Formulariossa2.id">
        <h4>{{ index +1 }}</h4>
        <Formulariossa2 :Formulariossa2="Formulariossa2" :showIdade="true" @meDelete="deletarUsuario ($event)"/>
      </div>
    </div>
  </div>
</template>

<script>
import _ from 'lodash';
import Formulariossa2 from './components/Formulariossa2';
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
      
      Formulariossa2s: [
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
    Formulariossa2, 
    Navbar,
    //Produto
  },
  methods:{
    cadastrarUsuario: function(){
      if(this.nomeField == "" || this.nomeField == "" || this.nomeField == "" || this.nomeField ==" " || this.nomeField ==" "< 0){
        this.deuErro = true;

      }else{
        this.Formulariossa2s.push({nome: this.nomeField, criancas6meses: this.criancasMenor6Meses, criancaAme: this.criancaAme, criancas2Anos: this.criancas2Anos, gestantes: this.gestantes, gestantesAte20Anos: this.gestantesAte20Anos, familias: this.familias, familiasAcompanhada: this.familiasAcompanhada})
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
      var id = $event.idDoFormulariossa2;
      var novoArray = this.Formulariossa2s.filter(Formulariossa2 => Formulariossa2.id != id);
      this.Formulariossa2s = novoArray;
      
    }
  },
  computed: {
    orderFormulariossa2s: function(){
            return _.orderBy(this.Formulariossa2s,['id'],['asc']);
    }
  }
}
</script>

<style>
  #nome-erro{
    color: red;
  }
</style>
